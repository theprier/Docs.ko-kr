---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 컨트롤러 추가 | Microsoft Docs
author: shanselman
description: 이 자습서는 여기 Visual Studio 2013을 사용 하 여 사용할 경우 업데이트 된 버전입니다. 새 자습서 t를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 하는 중...
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: afe1182bca0fe58e1df162c5027df35992eeef38
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809912"
---
<a name="adding-a-controller"></a>컨트롤러 추가
====================
[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다. 새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
> 
> 
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


MVC는 모델, 뷰, 컨트롤러를 나타냅니다. MVC에는 각 파트에는 서로 다른 책임을 응용 프로그램을 개발 하기 위한 패턴입니다.

- 데이터 응용 프로그램의 모델:
- 보기: 동적으로 HTML 응답을 생성 하려면 응용 프로그램에서 사용할 템플릿 파일입니다.
- 컨트롤러: 응용 프로그램에 들어오는 URL 요청을 처리 하는 클래스 모델 데이터를 검색 하 고 클라이언트에 다시 응답을 렌더링 하는 뷰 템플릿을 지정합니다

이 자습서에서 이러한 모든 개념을 다루는 수 하 고 응용 프로그램을 만들고 사용 하는 방법을 보여 됩니다.

솔루션 탐색기에서에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 컨트롤러 추가 선택 하 여 새 컨트롤러를 만들어 보겠습니다.

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

새 컨트롤러 "HelloWorldController" 이름과 추가 클릭 합니다.

[![컨트롤러 추가 대화 상자](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

HelloWorldController.cs 호출에 대해 만든 새 파일 및 해당 파일에 현재 열려 있는 오른쪽의 솔루션 탐색기에서 표시 합니다 **IDE**합니다.

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

다음과 같은 새 공용 클래스 HelloWorldController 내에서 두 개의 새 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 html 문자열로 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

컨트롤러 HelloWorldController 이름이 고 새로운 메서드가 인덱스 라고 합니다. 응용 프로그램을 다시 실행 전과 마찬가지로 (재생 단추를 클릭 하거나 f5 키를 눌러이 작업을 수행). 브라우저에 시작 되 면 주소 표시줄에서 경로 변경 `http://localhost:xx/HelloWorld` 여기서 xx는 무엇이 든 번호 컴퓨터 구성 했습니다. 이제 브라우저 아래 스크린샷 처럼 표시 됩니다. 위의 메서드를 반환 했습니다 "콘텐츠입니다." 라는 메서드로 전달 된 문자열 기억할지 시스템 일부 HTML을 반환 하 고 못해서!

ASP.NET MVC는 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 그 안에 다양 한 작업 메서드)를 호출합니다. ASP.NET MVC에서 사용 되는 매핑 논리 다음과 같은 형식을 사용 하 여 코드 실행 제어.

/[Controller]/[ActionName]/[Parameters]

URL의 첫 번째 부분 실행할 컨트롤러 클래스를 결정 합니다. 따라서 /HelloWorld HelloWorldController 클래스에 매핑됩니다. URL의 두 번째 부분 클래스에 대 한 작업 메서드를 결정 합니다. /HelloWorld/Index 없었다는 실행 HelloWorldcontroller 클래스의 index () 메서드. 만 위의 /HelloWorld 및 인덱스 암시 된 메서드를 방문 해야 함을 알 수 있습니다. 이 "Index" 라는 메서드를 명시적으로 지정 하지 않으면 컨트롤러에서 호출 되는 기본 방법 때문입니다.

[![내 기본 작업](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

이제 방문해 보도록 `http://localhost:xx/HelloWorld/Welcome.` 이제 시작 메서드는 실행 하 고 해당 HTML 문자열을 반환 합니다.

마찬가지로 / [Controller] / [ActionName] / [매개 변수] 컨트롤러 HelloWorld 이며 시작 메서드에 경우에 있도록 합니다. 매개 변수를 아직 완료 하지 것입니다.

[![이 시작 작업 방법](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

수정 해 보겠습니다 샘플 약간의 일부 정보를 URL에서 다음과 같은 예를 들어 컨트롤러에에 전달할 수 있도록: / HelloWorld/시작? name = Scott&amp;numtimes = 4. 두 매개 변수 및 아래와 같은 업데이트를 포함 하도록 시작 방법을 변경 합니다. 매개 변수 numTimes의 기본값은 1에서 전달 하지 않으면 나타내려면 C# 선택적 매개 변수 기능을 사용 했습니다에서는 note 합니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

응용 프로그램을 실행 하 고 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 원하는 이름과 numtimes의 값을 변경 합니다. 시스템에는 메서드의 매개 변수를 쿼리 문자열의 주소 표시줄에서 명명 된 매개 변수를 자동으로 매핑됩니다.

이러한 두 예제에서 컨트롤러 모든 작업을 수행 되었으며에 HTML을 직접 반환 되었습니다. 일반적으로 컨트롤러를 원하지는 종료 코드를 매우 불편 하므로 직접 HTML을 반환 합니다. 대신 일반적으로 별도 뷰 템플릿 파일을 HTML 응답을 생성 하는 데 사용 하겠습니다. 어떻게이 위해서는 살펴보겠습니다. 브라우저를 닫고 IDE에 반환 합니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part1.md)
> [다음](getting-started-with-mvc-part3.md)
