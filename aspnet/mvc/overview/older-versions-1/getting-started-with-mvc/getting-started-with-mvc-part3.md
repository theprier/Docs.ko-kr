---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: "뷰 추가 | Microsoft Docs"
author: shanselman
description: "ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 8725d054861c857ceac10a42b0cc3f2afe056aea
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="adding-a-view"></a>뷰 추가
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


이 섹션에서는 하겠습니다 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 생성 HTML 응답 캡슐화 HelloWorldController 클래스 수 있는 방법을 살펴보겠습니다.

이 인덱스 메서드로 템플릿 보기를 사용 하 여 시작 하겠습니다. 이 메서드는 인덱스 및는 HelloWorldController에 있습니다. 현재이 index () 메서드는 컨트롤러 클래스 내에서 하드 코드 된 메시지가 문자열을 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

이제 인덱스 메서드를 대신 다음과 같이 표시를 바꿔보겠습니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

Index () 메서드에 대 한 사용할 수 있는 프로젝트에 템플릿 보기를 지금 추가 해 보겠습니다. 이 수행 하려면 인덱스 메서드 중간 어딘가에 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 클릭...

![이미지](getting-started-with-mvc-part3/_static/image1.png)

그러면 우리 우리의 인덱스 메서드에 의해 사용할 수 있는 보기 템플릿을 만드는 하고자 하는 방법에 대 한 몇 가지 옵션을 제공 하 여 "뷰 추가" 대화 상자를 표시 됩니다. 지금은 없습니다 아무것도 변경 및 추가 단추를 클릭 합니다.

[![뷰 추가 대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

추가 클릭 한 후에 새 폴더 및 새 파일 나타납니다 솔루션 폴더에 다음 그림과 같이 합니다. 이제 해당 폴더 내의 보기 및 Index.aspx 파일에서 HelloWorld 폴더를 있습니다.

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

새 인덱스 파일 이기도 이미 열려 있고 편집을 위해 준비 합니다. 첫 번째에서 일부 텍스트 추가 &lt;h2&gt;인덱스&lt;/h2&gt; "Hello World."와 같은

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

ְ ְ ¿כ 방문 [ `http://localhost:xx/HelloWorld` ](http://localhostxx) 브라우저에서 다시 합니다. 이 예에서 컨트롤러 인덱스 메서드 한 작업을 수행 하지 않은 하지만 보기 템플릿 파일을 사용 하 여 클라이언트에 다시 응답을 렌더링 하 려 표시 "반환 View()" 호출 않았습니다. 사용할 보기 템플릿 파일의 이름, 명시적으로 지정 되지 않았기 때문에 ASP.NET MVC Index.aspx 뷰 파일을 사용 하 여 \Views\HelloWorld 폴더 내에 기본값입니다. 이제 우리 하드 코드 된 우리의 보기에서 문자열을 참조 합니다.

[![인덱스-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

잘 보입니다. 그러나 고 해당 데이터베이스는 브라우저의 제목 "Index" 라는 페이지에서 큰 제목에 "내 MVC 응용 프로그램입니다." 라고 표시 이러한 변경 해보겠습니다.

### <a name="changing-views-and-master-pages"></a>뷰 및 마스터 페이지를 변경합니다.

첫째, 바꿔보겠습니다 텍스트 "내 MVC 응용 프로그램입니다." 해당 텍스트를 공유 하 고 모든 페이지에 나타납니다. 실제로 나타납니다 한 위치를 코드에만 앱의 모든 페이지에는. 솔루션 탐색기에서 /Views/Shared 폴더 이동한 Site.Master 파일을 엽니다. 이 파일은 마스터 페이지 라고 하 고 공유 "셸" 우리의 다른 모든 페이지를 사용 하는 것이 있습니다.

이 파일의 일부 라는 텍스트를 "MainContent" ContentPlaceholder 확인 합니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

자리 표시자 위치를 만들면 모든 페이지 표시 됩니다, 마스터 페이지에 "래핑되어"입니다. 바꾸려고 제목, 응용 프로그램을 실행 하 고 여러 페이지를 방문 합니다. 하나의 변경 내용을 여러 페이지에 표시 되는지 확인할 수 있습니다.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

"내 MVC 영화 응용 프로그램입니다.."의 H1-이제 모든 페이지를 기본 제목-갖습니다입니다. 위쪽에 있는 모든 페이지에서 공유 되는 흰색 텍스트를 처리 하는입니다.

이 변경 된 제목으로 한 번에는 Site.Master 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

이제 인덱스 페이지의 제목을 변경 해보겠습니다.

/HelloWorld/Index.aspx를 엽니다. 두 곳 변경할 수 있습니다. 첫째, 제목에에서 나타나는 보조 헤더-도 h-2에는 브라우저의 제목입니다. 각 비트는 코드를 확인할 수 있도록 약간 다른 응용 프로그램의 어느 부분이 변경 시킬 겁니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

응용 프로그램을 실행 하 고 /Movies를 방문 합니다. 브라우저의 제목, 기본 제목 및 작은 제목을 변경 되었습니다. 확인 합니다. 크게 변경 약간 변경 된 응용 프로그램에서 보기에 두는 것이 쉽습니다.

[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

우리의 약간 (이 경우 "Hello World!"의 "데이터"의 그러나 코딩 된 메시지)는 하드입니다. V (Views) 준비 하 고 C (컨트롤러) 하지만 없는 M (모델) 아직 접수 했습니다. 방법 곧 살펴봅니다 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-a-viewmodel"></a>ViewModel 전달

데이터베이스를 이동 하 고 모델에 대해 설명 하는, 그러나 처음에 대해 살펴보기 "Viewmodel입니다." 이들은 HTML 응답을 클라이언트로 다시 렌더링 해야 하는 뷰 템플릿을 나타내는 개체입니다. 일반적으로 만들어지는 및 템플릿 보기에는 컨트롤러 클래스에 의해 전달 하며 뷰 템플릿에 필요한-데이터와 더 이상 포함 해야 합니다.

이전에 HelloWorld 샘플의 경우와 우리의 Welcome() 동작 메서드는 이름과 numTimes 매개 변수 하 고 브라우저에 출력. 이 응답을 직접 렌더링 하 계속 컨트롤러를 갖는 대신 대신 만들어 보겠습니다 데이터를 저장 하 고 다시 사용 하 여 HTML 응답을 렌더링 하는 보기 템플릿을를 통해 전달 하기 위한 작은 클래스. 컨트롤러는 한 가지 및 템플릿 보기와 관련 되어 이러한 방식으로 다른 – 정리 "문제의 분리" 응용 프로그램 내에서 유지 관리를 사용 하도록 설정 합니다.

HelloWorldController.cs 파일을 반환 하 고 새 "WelcomeViewModel" 클래스를 추가 하 고 컨트롤러 내 시작 방법을 변경. 다음은 동일한 파일에서 새 클래스와 함께 전체 HelloWorldController.cs입니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

여러 줄에는 것이 시작 방법은 실제로 두 개의 코드 문을 합니다. ViewModel 개체 및 두 번째 단계에는 두 개의 매개 변수를 결과 개체 보기에 패키지 하는 첫 번째 문입니다.

이제 시작 뷰 템플릿이 필요 합니다! 시작 메서드에서 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 선택 합니다. 이 시간 확인 "강력한 형식의 뷰 만들기" 알아보고 하겠습니다 WelcomeViewModel 클래스 드롭 다운 목록에서에서 선택. 이 새 보기 WelcomeViewModels 및 다른 형식의 개체에 대 한만 알게 됩니다.

> *참고: 드롭다운 목록에에서 표시에 대 한 프로그램 WelcomeViewModel을 추가한 후 한 번 컴파일한 해야 합니다.*


뷰 추가 대화 상자에는 모양은 다음과 같습니다. 추가 단추를 클릭 합니다. ![보기 원으로 표시 추가](getting-started-with-mvc-part3/_static/image10.png)

아래이 코드를 추가 &lt;h2&gt; 프로그램 새 Welcome.aspx에 있습니다. 사용자가 중요 횟수 만큼 Hello 말 알아보고 루프 확인 하겠습니다!

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

또한이 뷰는 WelcomeViewModel에 대 한 말씀 때문에 입력 하는 동안 확인 (결혼 여부는, 기억?) 될 때마다를 참조 하는 모델 개체 아래 스크린샷에서 보듯이 유용한 Intellisense을 얻기:

[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

ְ ְ ¿כ 방문 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 다시 합니다. त ु म 데이터 URL에서, 이제 Controller에 자동 전달, Controller는 ViewModel으로 데이터를 패키지 하 고이 보기에 해당 개체를 전달 합니다. 사용자에 게 데이터를 HTML로 표시 하는 보다 보기입니다.

[![Windows Internet Explorer-시작](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

이 였 종류를 모델에 대 한 "M"의 하지만 데이터베이스 종류 되지 않습니다. 지금까지 학습 및 기능 영화 데이터베이스를 만들 보겠습니다.

>[!div class="step-by-step"]
[이전](getting-started-with-mvc-part2.md)
[다음](getting-started-with-mvc-part4.md)
