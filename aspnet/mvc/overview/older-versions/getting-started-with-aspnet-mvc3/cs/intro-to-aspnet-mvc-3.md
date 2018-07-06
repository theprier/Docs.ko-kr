---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: b0ff8da1911b36e6e74e5c7057f27d891ad57f61
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832291"
---
<a name="intro-to-aspnet-mvc-3-c"></a>ASP.NET MVC 3 (C#) 소개
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [C# 버전 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


## <a name="what-youll-build"></a>만들 내용

만들기, 편집 및 나열 하는 데이터베이스에서 동영상을 지 원하는 간단한 영화 목록 응용 프로그램을 구현할 수 있습니다. 다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다. 데이터베이스에서 동영상 목록을 표시 하는 페이지가 포함 됩니다.

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

또한 응용 프로그램 추가, 편집 및 개별 문제에 대 한 참조 정보 뿐만 아니라 영화를 삭제할 수 있습니다. 데이터베이스에 저장 된 데이터가 올바른지 확인 하려면 유효성 검사를 포함 하는 모든 데이터 입력 시나리오입니다.

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>학습할 기술

학습할 다음과 같습니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법입니다.
- 컨트롤러 및 보기에는 ASP.NET MVC를 만드는 방법입니다.
- Entity Framework Code First 패러다임을 사용 하 여 새 데이터베이스를 만드는 방법입니다.
- 검색 데이터를 표시 하는 방법입니다.
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법.

## <a name="getting-started"></a>시작

Visual Web Developer 2010 Express ("Visual Web Developer" 줄여서)를 실행 하 여 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.

Visual Web Developer에는 IDE 또는 통합된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다. Visual Web Developer에서 사용할 수 있는 다양 한 옵션을 보여 주는 맨 위에 있는 도구 모음이 있습니다. IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다. (예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

Visual Basic 또는 Visual C# 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다. 왼쪽의 Visual C#을 선택 하 고 선택한 **ASP.NET MVC 3 웹 응용 프로그램**합니다. "MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다. (Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의.)

![](intro-to-aspnet-mvc-3/_static/image5.png)

에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다. 확인할 **태그를 사용 하 여 HTML5** 두고 **Razor** 기본 뷰 엔진으로 합니다.

![](intro-to-aspnet-mvc-3/_static/image6.png)

**확인**을 클릭합니다. 있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Web Developer! 이는 간단한 "Hello World!" 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.

![](intro-to-aspnet-mvc-3/_static/image9.png)

디버깅을 시작 하려면 바로 가기 키 F5 인지 확인 합니다.

F5 Visual Web Developer는 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다. 그런 다음 visual Web Developer는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost` 등은 표시 되지 않습니다 및 `example.com`합니다. 있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다. Visual Web Developer에서 웹 프로젝트를 실행 하면 임의 포트를 웹 서버에 사용 됩니다. 아래 이미지에서 임의 포트 번호가 43246입니다. 응용 프로그램을 실행 하는 경우 아마도 다른 포트 번호를 표시 됩니다.

![](intro-to-aspnet-mvc-3/_static/image10.png)

즉시이 기본 템플릿을 사용 하면 두 페이지를 방문 하 고 기본 로그인 페이지입니다. 다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 진행에서 하는 것입니다. 브라우저를 닫고 몇 가지 코드를 변경해 보겠습니다.

> [!div class="step-by-step"]
> [다음](adding-a-controller.md)
