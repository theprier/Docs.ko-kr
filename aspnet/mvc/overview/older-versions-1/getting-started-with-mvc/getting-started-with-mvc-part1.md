---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 소개 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 3dda4701c9be90bea7c95a330845d601345ac46b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834820"
---
<a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 소개
====================
[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
> 
> 
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


사용 하 여 첫 ASP.NET MVC 웹 응용 프로그램을 만들어 보겠습니다 [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)합니다. 보겠습니다 만들고 영화를 나열 하는 간단한 영화 목록 응용 프로그램을 만들어 보겠습니다.

## <a name="what-youll-build"></a>만들 내용

다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다. 다양 한 열을 사용 하 여 동영상의 간단한 테이블을 해야 합니다.

[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

및 영화 목록에 추가할 수 있도록 만드는 폼을 해야 합니다.

[![동영상-Windows Internet Explorer (2) 만들기](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>학습할 기술

이 자습서는 Visual Studio를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 알아봅니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법
- SQL Server를 사용 하 여 새 데이터베이스를 만드는 방법
- ASP.NET MVC 컨트롤러 및 보기를 만드는 방법
- 검색 데이터를 표시 하는 방법
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법
- 데이터베이스 스키마를 업데이트 하는 방법

## <a name="get-started"></a>시작

시작 화면에서 Visual Web Developer 2010 Express (부르겠습니다 "VWD" 지금부터) 선택한 새 프로젝트를 실행 하 여 시작 합니다.

Visual Web Developer에는 IDE 또는 통합 개발자 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다. 파일 선택를 사용할 수도 있습니다 메뉴 뿐만 아니라, 사용 가능한 여러 옵션을 보여 주는 위에 도구 모음 | 새 프로젝트입니다.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

Visual Basic 또는 Visual C#을 사용 하 여 응용 프로그램을 만들 수 있습니다. 이제 선택 Visual C# 왼쪽에서 선택 "ASP.NET MVC 2 웹 응용 프로그램입니다." 프로젝트 "Movies" 이름을 지정 하 고 확인을 클릭 합니다.

[![새 프로젝트](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

오른쪽에 응용 프로그램에서 모든 파일 및 폴더를 보여 주는 솔루션 탐색기. 중간에 큰 기간은 코드를 편집 하 고 대부분의 시간입니다. 있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio! 이 간단한 "Hello World! 프로젝트 되며 응용 프로그램을 시작 하는 것이 좋습니다.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

도구 모음에 "재생" 단추를 선택 합니다.

![디버깅 시작](getting-started-with-mvc-part1/_static/image11.png)

프로그램을 컴파일하고 웹 브라우저에서 응용 프로그램을 시작 하는 오른쪽을 가리키는 녹색 화살표는 것입니다.

*참고: 있습니다 수 대신 키보드에서 f5 키를 누르거나 디버그-&gt;"디버그" 메뉴에서 디버깅 시작 합니다.*

이렇게 하면 Visual Web Developer는 개발 웹 서버를 시작 하 고 (구성 또는이 기능을 사용 하는 데 필요한 수동 단계 없는 함) 웹 응용 프로그램을 실행 합니다. 그런 다음 브라우저를 시작 하 고 응용 프로그램의 홈 페이지로 이동 하도록 구성 합니다. 아래는 브라우저의 주소 표시줄 코드는 "localhost" example.com 같이 하지 확인 합니다. Localhost는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터-항상 가리키는 때문입니다.

[![홈 페이지](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

기본적으로이 기본 템플릿은 있습니다 두 페이지를 방문 하 고 기본 로그인 페이지를 제공 합니다. 보겠습니다이 응용 프로그램의 작동 방식을 변경할 조금 더 자세히 알아보고 ASP.NET MVC 진행에서 합니다. 브라우저를 닫고 몇 가지 코드를 변경할 수 있습니다.

> [!div class="step-by-step"]
> [다음](getting-started-with-mvc-part2.md)
