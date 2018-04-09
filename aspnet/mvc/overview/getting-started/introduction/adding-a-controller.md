---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 3864bab284661b0c44f9e4cb363c2d60eccc7c66
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-controller"></a>컨트롤러 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

MVC는 *모델-뷰-컨트롤러*합니다. MVC는은 잘 설계, 테스트 및 유지 관리 하기 쉬운 응용 프로그램을 개발 하기 위한 패턴입니다. MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.

- **M** odels: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하 고 응용 프로그램의 데이터를 나타내는 클래스입니다.
- **V** iews: 응용 프로그램 사용 HTML 응답을 동적으로 생성 하는 템플릿 파일입니다.
- **C** ontrollers: 들어오는 브라우저 요청을 처리 하는 클래스 모델 데이터를 검색 한 다음 브라우저에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.

이 자습서 시리즈의 이러한 모든 개념을 다루는 수 알아보고 응용 프로그램을 만들고이 사용 하는 방법을 설명 하겠습니다.

> [!NOTE]
> 기본 MVC 이전 단계에서 템플릿을 선택 했습니다. 이 나타나고 가정, 계정 컨트롤러 기본적으로 관리 합니다.

컨트롤러 클래스를 만들어 시작 해 보겠습니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더와 클릭 **추가**, 다음 **컨트롤러**합니다.


![](adding-a-controller/_static/image1.png)

에 **스 캐 폴드를 추가** 대화 상자를 클릭 **MVC 5 컨트롤러-비어 있지**, 클릭 하 고 **추가**합니다.

![](adding-a-controller/_static/image2.png)  
 

"HelloWorldController" 새 컨트롤러 이름을 지정 하 고 클릭 **추가**합니다.

![컨트롤러 추가](adding-a-controller/_static/image3.png)

**솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs* 와 새 폴더 *Views\HelloWorld*합니다. 컨트롤러는 IDE에 열려 있습니다.

![](adding-a-controller/_static/image4.png)

파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

예를 들어 컨트롤러 메서드에 html 문자열을 반환 합니다. 컨트롤러 이름은 `HelloWorldController` 첫 번째 메서드는 이름이 고 `Index`합니다. 브라우저에서 호출 해 보겠습니다. (누름 F5 또는 Ctrl + F5) 응용 프로그램을 실행 합니다. 브라우저에서 추가 &quot;HelloWorld&quot; 주소 표시줄에 경로에 있습니다. (의 아래 그림의 예를 들어 `http://localhost:1234/HelloWorld.`) 브라우저에서 페이지는 다음 스크린샷과 같이 표시 됩니다. 위의 메서드 코드 문자열이 직접 반환 합니다. 일부 HTML 반환할을 시스템에서 설정한 다시!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 다른 작업 메서드 내에서)를 호출합니다. ASP.NET MVC에서 사용 하는 기본 URL 라우팅 논리를 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 합니다.

`/[Controller]/[ActionName]/[Parameters]`

라우팅에 형식을 설정한는 *앱\_Start/RouteConfig.cs* 파일입니다.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

응용 프로그램을 실행 하 고 모든 URL 세그먼트를 제공 하지 마십시오 "Home" 컨트롤러에 기본적으로 고 "Index" 작업 메서드의 위 코드의 기본값 섹션에 지정 합니다.

URL의 첫 번째 부분 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 으 리라 예상는 `Index` 의 메서드는 `HelloWorldController` 실행 하는 클래스입니다. 로 이동 했습니다 사라졌는지 */HelloWorld* 및 `Index` 기본적으로 메서드를 사용 합니다. 라는 메서드가 때문에 이것이 `Index` 은 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 방법입니다. URL 세그먼트(`Parameters`)의 세 번째 부분은 경로 데이터입니다. 이 자습서에서 경로 데이터를 나중에 표시 됩니다 했습니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. `Welcome` 메서드가 실행 되 고 문자열을 반환 &quot;이 시작 작업 방법... &quot;. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.

![](adding-a-controller/_static/image6.png)

수정 해 보겠습니다 예제 약간를 컨트롤러에 URL에서 일부 매개 변수 정보를 전달할 수 있습니다 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*). 변경 하면 `Welcome` 메서드를 다음과 같이 두 개의 매개 변수를 포함 합니다. 코드는 C# 기능 선택적 매개 변수를 사용 하 여 임을 나타내는 참고는 `numTimes` 경우 해당 매개 변수에 대해 값은 1의 매개 변수 기본값은입니다.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> 보안 참고: 사용 하 여 위의 코드 [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) 악의적인 입력 (즉 JavaScript)에서 응용 프로그램을 보호 합니다. 자세한 내용은 참조 [하는 방법: 보호에 대 한 스크립트에 의해 악용 문자열을 HTML 인코딩 적용 하 여 웹 응용 프로그램에서](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)합니다.


 ְ ְ ¿כ 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`). 에 대해 다른 값을 시도할 수 `name` 및 `numtimes` url에서입니다. [ASP.NET MVC 모델 바인딩 시스템이](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 메서드의 매개 변수에 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image7.png)

URL 세그먼트 위의 샘플에서 ( `Parameters`)을 사용 하지 않으면는 `name` 및 `numTimes` 매개 변수가 전달 [쿼리 문자열을](http://en.wikipedia.org/wiki/Query_string)합니다. ? (물음표)는 위 URL에서는 한 구분 기호 및 쿼리 문자열에 따라 합니다. &amp; 문자는 쿼리 문자열을 구분합니다.

시작 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

응용 프로그램을 실행 하 고 다음 URL을 입력 합니다. `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

이 이번 세 번째 URL 세그먼트 일치 경로 매개 변수 `ID.` 는 `Welcome` 동작 메서드에 매개 변수를 포함 (`ID`) URL 사양에 일치 하는 `RegisterRoutes` 메서드.

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC 응용 프로그램의 일반적인 쿼리 문자열로 전달 보다 경로 데이터 (예: 위의 id에 수행한)와 매개 변수를 전달 하는 합니다. 또한 모두 전달에 대 한 경로 추가할 수 있습니다는 `name` 및 `numtimes` URL에 대 한 경로 데이터와 매개 변수에서 합니다. 에 *앱\_Start\RouteConfig.cs* 파일에서 "Hello" 경로 추가:

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

응용 프로그램을 실행 하 고 찾아보기 `/localhost:XXX/HelloWorld/Welcome/Scott/3`합니다.

![](adding-a-controller/_static/image9.png)

대부분의 MVC 응용 프로그램 기본 경로 제대로 작동합니다. 모델 바인더를 사용 하 여 데이터를 전달 하기 위해이 자습서의 뒷부분에 나오는 배웁니다 및에 대 한 기본 경로 수정할 필요가 없습니다.

다음 예에서 컨트롤러는 작업을 하 고는 &quot;VC&quot; MVC의 부분 — 뷰와 컨트롤러 작업 즉, 합니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 코드에 번거로운 되므로 HTML을 직접 반환 하는 컨트롤러 않으려는 합니다. 대신 일반적으로에서는 별도 뷰를 서식 파일을 HTML 응답을 생성할 수 있도록 합니다. 다음 방법을 수행 수에 대해 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started.md)
> [다음](adding-a-view.md)
