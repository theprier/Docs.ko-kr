---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 컨트롤러 추가 | Microsoft Docs
author: shanselman
description: 이 자습서는 다음 Visual Studio 2013을 사용 하 여 사용할 수 있는 경우 업데이트 된 버전입니다. T 보다 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 하는 새 자습서 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: c6ecd1ffdd53a629d0079d57b85c7f6db2f316ce
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869025"
---
<a name="adding-a-controller"></a>컨트롤러 추가
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 이 자습서를 사용할 수 있는 경우 업데이트 된 버전 [여기](../../getting-started/introduction/getting-started.md) 를 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
> 
> 
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


MVC는 모델, 뷰, 컨트롤러를 나타냅니다. MVC에는 각 파트에는 서로 다른 책임 되도록 응용 프로그램을 개발 하기 위한 패턴입니다.

- 데이터 응용 프로그램의 모델:
- 보기: HTML 응답을 동적으로 생성 하 여 응용 프로그램에서 사용할 템플릿 파일입니다.
- 컨트롤러의 경우: 응용 프로그램에서 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 한 다음 다시 클라이언트에 대 한 응답을 렌더링 하는 템플릿 보기를 지정

이 자습서에서는 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.

솔루션 탐색기의에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 컨트롤러 추가 선택 하 여 새 컨트롤러를 만들어 보겠습니다.

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

새 컨트롤러 "HelloWorldController" 이름을 지정 하 고 추가 클릭 합니다.

[![컨트롤러 추가 대화 상자](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

HelloWorldController.cs 호출한 경우에 대 한 새 파일을 만든 하에서 해당 파일을 열면 이제 오른쪽의 솔루션 탐색기에서 공지는 **IDE**합니다.

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

다음과 같은 새 공용 클래스 HelloWorldController 안에 두 개의 새 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

컨트롤러 이름이 HelloWorldController이 고 새로운 메서드가 인덱스 라고 합니다. 응용 프로그램을 다시 실행 이전과 동일 하 게 (재생 단추를 클릭 하거나 f5 키를 눌러이 작업을 수행). 브라우저 시작 된 후 주소 표시줄에서 경로 변경 `http://localhost:xx/HelloWorld` 여기서 xx는 무엇이 든 컴퓨터 번호를 구성 했습니다. 이제 브라우저가 아래 스크린샷과 같이 표시 됩니다. 위의 메서드에서 म 반환 "콘텐츠입니다." 라는 메서드로 전달 된 문자열 시스템에만 일부 HTML 반환 다시를 말!

ASP.NET MVC 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다. ASP.NET MVC에서 사용 하는 기본 매핑 논리 다음과 같은 형식을 사용 하 여 코드 실행을 제어.

/[Controller]/[ActionName]/[Parameters]

URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다. 따라서 /HelloWorld HelloWorldController 클래스에 매핑됩니다. URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다. 따라서 /HelloWorld/Index index () 메서드를 실행할 HelloWorldcontroller 클래스의 리라 예상 되었습니다. 만 위의 /HelloWorld 및 인덱스 유추 되었으므로 메서드 방문 야 했음을 확인 합니다. 즉, "Index" 라는 메서드를 명시적으로 지정 하지 않으면 컨트롤러에 호출한 기본 방법입니다.

[![내 기본 작업](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

이제 보겠습니다 방문 `http://localhost:xx/HelloWorld/Welcome.` 이제 시작 메서드에 실행 되 고 해당 HTML 문자열을 반환 했습니다.

다시 / [컨트롤러] / [ActionName] / [매개 변수] 없으므로 컨트롤러는 HelloWorld가 메서드가 경우 시작 합니다. 매개 변수를 아직 수행 하지 않은 것입니다.

[![이 시작 작업 방법](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

수정 해 보겠습니다 샘플 약간의 일부 정보 URL에서 다음과 같은 예를 들어 컨트롤러에 전달할 수 있도록: / HelloWorld/시작? name = Scott&amp;numtimes = 4. 두 개의 매개 변수 및 다음과 유사한 업데이트를 포함 하도록 시작 방법을 변경 합니다. Note 있는지는 매개 변수 numTimes의 기본값은 1에서 전달 되지 않은 경우를 나타내기 위해 C# 선택적 매개 변수 기능을 사용 했습니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

ְ ְ ¿כ 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 원하는 만큼 이름과 numtimes의 값을 변경 합니다. 시스템 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑됩니다.

두이 예제에서 컨트롤러는 모든 작업을 수행 하 되 고에 HTML을 직접 반환 되었습니다. 일반적으로 우리의 컨트롤러 않도록 하는 코드에 번거로운 되 고 결국 이후 직접-HTML을 반환 합니다. 대신 일반적으로에서는 별도 템플릿 파일 보기 HTML 응답을 생성 하기. 어떻게 이렇게 하려면 살펴보겠습니다. 브라우저를 닫고 IDE로 돌아갑니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part1.md)
> [다음](getting-started-with-mvc-part3.md)
