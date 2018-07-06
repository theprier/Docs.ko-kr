---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 뷰 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: e3b923aa5572781261c5a75546700faf223703d4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834506"
---
<a name="adding-a-view"></a>뷰 추가
====================
[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다. 방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.


이 섹션에서는 하겠습니다 뷰 템플릿 파일을 완전히 다시 클라이언트에 HTML 응답을 생성을 캡슐화 하는 데 HelloWorldController 클래스를 가질 수 방법을 살펴보겠습니다.

인덱스 메서드에 보기 템플릿을 사용 하 여 시작 해 보겠습니다. 이 메서드는 인덱스 이며 HelloWorldController 합니다. 현재 index () 메서드는 컨트롤러 클래스 내에서 하드 코딩 된 메시지를 사용 하 여 문자열을 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

인덱스 방법 대신 다음과 같이 이제 변경해 보겠습니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

Index () 메서드를 사용할 수 있는 프로젝트를 뷰 템플릿으로 지금 추가 하겠습니다. 이렇게 하려면 인덱스 메서드에 중간 어딘가에 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 클릭 하는 중...

![이미지](getting-started-with-mvc-part3/_static/image1.png)

우리는 인덱스 메서드에서 사용할 수 있는 보기 템플릿을 만들려고 하는 방법에 대 한 몇 가지 옵션을 제공 하는 "뷰 추가" 대화 상자가 표시 됩니다. 지금은 없습니다 아무것도 변경 및 추가 단추를 클릭 합니다.

[![뷰 추가 대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

추가 클릭 하면 새 폴더 및 새 파일 나타납니다 솔루션 폴더에 다음과 같이 합니다. 이제 뷰 및 Index.aspx 파일에 HelloWorld 폴더를 해당 폴더 내에 있어야 합니다.

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

새 인덱스 파일이 이미 열린 및 편집을 위해 준비 합니다. 첫 번째 텍스트를 추가 &lt;h2&gt;인덱스&lt;/h2&gt; "Hello World."와 같은

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

응용 프로그램을 실행 하 고 방문 [ `http://localhost:xx/HelloWorld` ](http://localhostxx) 브라우저에서 다시 합니다. 이 예제에서 컨트롤러의 인덱스 메서드에서 모든 작업을 수행 하지 않은 하지만 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 응답을 렌더링 하려고 했습니다 나타내는 "반환 View()"를 호출 하지 못했습니다. 에서는 않았습니다 지정 하지 않으므로 명시적으로 사용 하 여 뷰 템플릿 파일의 이름, Index.aspx 뷰 파일을 사용 하 여 \Views\HelloWorld 폴더 내에 ASP.NET MVC 기본값입니다. 이제에서는 하드 코드 된 뷰에 문자열이 표시 했습니다.

[![Windows Internet Explorer 인덱스](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

잘 찾습니다. 그러나 브라우저의 제목 "Index" 라는 페이지의 큰 제목에 "내 MVC 응용 프로그램입니다." 라는 것을 알합니다 이러한 파일을 변경해 보겠습니다.

### <a name="changing-views-and-master-pages"></a>보기 및 마스터 페이지를 변경합니다.

먼저 텍스트 "내 MVC 응용 프로그램입니다."을 변경해 보겠습니다 해당 텍스트를 공유 하 고 모든 페이지에 표시 됩니다. 실제로 나타나는 곳 에서만 코드를 앱에서 모든 페이지에도 합니다. 솔루션 탐색기에서 /Views/Shared 폴더로 이동한 Site.Master 파일을 엽니다. 이 파일은 마스터 페이지 라고 하 고 공유 "셸"는 다른 모든 페이지를 사용 하는 것입니다.

이 파일의 ContentPlaceholder "MainContent" 라는 텍스트를 확인 합니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

자리 표시자 이며 여기서 만든 모든 페이지 표시 됩니다, 마스터 페이지에 "래핑된" 앱을 실행 하 고 여러 페이지를 방문 제목을 변경을 시도 합니다. 하나의 변경 내용을 여러 페이지에 표시 되는지 확인할 수 있습니다.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

H1-"내 MVC 동영상 응용 프로그램입니다."의 모든 페이지를 기본 제목-이제는 맨 위쪽에 있는 모든 페이지 간에 공유 되는 흰색 텍스트를 처리 하는 합니다.

변경 된 제목이 사용 하 여 전체에서 Site.Master 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

이제 인덱스 페이지의 제목을 변경 해보겠습니다.

/HelloWorld/Index.aspx를 엽니다. 변경 하려면 두 위치 있습니다. 첫째, 제목에에서 나타나는 보조 머리글도 H2-는 브라우저의 제목입니다. 만들겠습니다 각각는 약간의 코드를 볼 수 있도록 약간 다른 앱의 어느 부분을 변경 합니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

앱을 실행 하 고 /Movies를 참조 하세요. 브라우저 제목, 기본 제목 및 작은 제목이 변경 되었습니다. 알 수 있습니다. 보기에 작은 변경 내용을 사용 하 여 앱에서 큰 변화를 확인 하기 쉽습니다.

[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

우리의 약간 (이 경우 "Hello World!"의 "데이터"의 메시지)는 하드 코딩 하지만입니다. 했습니다 V (뷰) 및 C (컨트롤러) 하지만 없습니다 M (모델) 아직를 만들었습니다. 방법을 곧 살펴보겠습니다 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-a-viewmodel"></a>ViewModel을 전달합니다.

전에 데이터베이스를 이동 하 고 모델에 대 한 설명, 그러나 처음에 대해 살펴보겠습니다 "Viewmodel"로 지정 합니다. 이 클라이언트에 HTML 응답을 렌더링 해야 하는 뷰 템플릿을 나타내는 개체입니다. 일반적으로 생성 됩니다 및 템플릿 보기, 컨트롤러 클래스에 의해 전달 하며 보기 템플릿이 필요 하며 받는 데이터 및 더 이상 포함 해야 합니다.

이전에 HelloWorld 샘플을 사용 하 여이 Welcome() 작업 메서드 이름과 numTimes 매개 변수는 데 걸린 및 브라우저에 출력 합니다. 계속 직접이 응답을 렌더링 하는 컨트롤러에 있는 것이 아니라 대신 보겠습니다 작은 클래스를를 해당 데이터를 보유할 보기 템플릿을 사용 하 여 HTML 응답을 렌더링 하를 전달 합니다. 컨트롤러 보기 템플릿에서 한 가지와 관련이이 이렇게 다른 – 정리 "문제의 분리" 응용 프로그램 내에서 유지 관리를 사용 하도록 설정 합니다.

HelloWorldController.cs 파일 및 새 "WelcomeViewModel" 클래스를 추가 돌아가서 컨트롤러 내에서 시작 하는 방법을 변경 합니다. 동일한 파일에서 새 클래스를 사용 하 여 전체 HelloWorldController.cs 다음과 같습니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

여러 줄에 있는 경우에이 시작 방법은 실제로 두 개의 코드 문을입니다. 첫 번째 문은 결과 개체 보기를 ViewModel 개체에 두 번째 패스는 두 매개 변수를 패키지 합니다.

이제 시작 보기 템플릿이 필요 합니다! 시작 메서드를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가 선택 합니다. 이 이번에 됩니다 "강력한 형식의 뷰 만들기"를 확인 하 고 드롭다운 목록에서에서 WelcomeViewModel 클래스를 선택 합니다. 이 새 보기는 WelcomeViewModels 및 다른 종류의 개체에 대해서만 인식 됩니다.

> *참고: 드롭다운 목록에에서 표시에 대 한 프로그램 WelcomeViewModel 추가 후 한 번 컴파일한 해야 합니다.*


뷰 추가 대화 상자 모양을 다음과 같습니다. 추가 단추를 클릭 합니다. ![보기 원으로 표시 추가](getting-started-with-mvc-part3/_static/image10.png)

아래에이 코드를 추가 합니다 &lt;h2&gt; 에 새 Welcome.aspx에서. 루프를 확인 하 고 사용자가 해야 만큼 살펴보기 드리겠습니다!

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

또한 기억할지이 WelcomeViewModel에 대 한 보기 때문에 입력 하는 동안 확인 (결혼 여부는, 기억?)은 모델 개체 아래 스크린샷에 표시 된 참조 될 때마다 유용한 Intellisense를 시작 하기:

[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

응용 프로그램을 실행 하 고 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 다시 합니다. URL에서 데이터 취하고 이제 자동으로 컨트롤러에 전달 될, 컨트롤러 ViewModel에 대 한 데이터를 패키지 하 고 보기에 해당 개체를 전달 합니다. 사용자에 게 HTML로 데이터를 표시 하는 보다 뷰.

[![시작-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

물론 특정 유형의 모델에 대 한 "M" 이지만 데이터베이스 유형은 하지 했습니다. 새로운 지금까지 학습 한 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part2.md)
> [다음](getting-started-with-mvc-part4.md)
