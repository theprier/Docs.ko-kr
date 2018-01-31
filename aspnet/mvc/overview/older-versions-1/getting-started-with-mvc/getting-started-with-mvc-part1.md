---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: "ASP.NET MVC 소개 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 08c30f4aab77bff64ed3ab874d13cc5dc863fc99
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 소개
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 이 자습서를 사용할 수 있는 경우 업데이트 된 버전 [여기](../../getting-started/introduction/getting-started.md) 를 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
> 
> 
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


사용 하 여 첫 번째 ASP.NET MVC 웹 응용 프로그램을 만들어 보겠습니다 [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)합니다. 약간 영화 목록 응용 프로그램을 알려 주세요 만들고 영화 목록 확인 합니다.

## <a name="what-youll-build"></a>만들 것인지

다음은 빌드합니다.이 응용 프로그램의 두 가지 스크린샷입니다. 간단한 테이블 다양 한 열을 사용 하 여 동영상을 갖습니다.

[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

및 양식 만들기 해야 하므로 동영상 목록에 추가할 수 있습니다.

[![동영상-Windows Internet Explorer (2) 만들기](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>기술을 알아봅니다

이 자습서에서는 Visual Studio를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 배웁니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법
- SQL Server와 함께 새 데이터베이스를 만드는 방법
- ASP.NET MVC 컨트롤러와 뷰를 만드는 방법
- 검색 한 데이터를 표시 하는 방법
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하는 방법
- 데이터베이스 스키마를 업데이트 하는 방법

## <a name="get-started"></a>시작

시작 화면에서 Visual Web Developer 2010 Express (부르겠습니다 "VWD" 지금부터) 및 선택 새 프로젝트를 실행 하 여 시작 합니다.

Visual Web Developer IDE 또는 통합 개발자 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 있는 IDE를 사용 합니다. 도구 모음,으로 수 또한를 사용 하 여 파일을 선택 하 고 메뉴를 사용할 수 있는 다양 한 옵션을 보여 주는: 위쪽 | 새 프로젝트입니다.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

Visual Basic 또는 Visual C#을 사용 하 여 응용 프로그램을 만들 수 있습니다. 지금은 선택 Visual C#의 왼쪽에서 선택 "ASP.NET MVC 2 웹 응용 프로그램입니다." 프로젝트 "영화" 이름을 지정 하 고 확인을 클릭 합니다.

[![새 프로젝트](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

오른쪽에는 응용 프로그램에서 모든 파일 및 폴더를 보여 주는 솔루션 탐색기입니다. 가운데 있는 큰 창은 코드를 편집 하 고 대부분의 시간을 소비는 합니다. Visual Studio 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 서식 파일을 사용 해야 하므로 응용 프로그램 현재 아무것도 수행 하지 않고! 이 간단한 "Hello World! 프로젝트를 되며 응용 프로그램에 대 한 시작 하는 것이 좋습니다.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

도구 모음에 있는 "재생" 단추를 선택 합니다.

![디버깅 시작](getting-started-with-mvc-part1/_static/image11.png)

프로그램을 컴파일하고 웹 브라우저에서 응용 프로그램을 시작 하는 오른쪽을 가리키는 녹색 화살표는

*참고: 수 대신 F5 키보드에 누르거나 선택 하면 디버그-&gt;"디버그" 메뉴에서 디버깅 시작 합니다.*

이렇게 하면 Visual Web Developer 개발 웹 서버를 시작 하 고 (구성 또는이 기능을 사용 하는 데 필요한 수동 단계가 없는 함) 웹 응용 프로그램을 실행 합니다. 그런 다음 브라우저 시작 되며 응용 프로그램의 홈 페이지를 검색 하도록 구성 합니다. 아래 "localhost" 및 다음과 example.com 같이 브라우저의 주소 표시줄 표시 있는지 확인 합니다. 항상 로컬 컴퓨터-방금 빌드한 응용 프로그램을 실행 중인이 예제의 localhost를 가리키는 때문입니다.

[![홈 페이지](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

즉시 이러한 기본 템플릿은 하면 두 개의 페이지를 방문 하 고 기본 로그인 페이지를 제공 합니다. 이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간 배우 살펴보겠습니다. 브라우저를 닫고 일부 코드를 변경할 수 있습니다.

>[!div class="step-by-step"]
[다음](getting-started-with-mvc-part2.md)
