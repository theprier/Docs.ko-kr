---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 77389bfa4774857eb2a607b0a70e982826312e03
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802294"
---
<a name="adding-a-controller"></a>컨트롤러 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

MVC는 의미 *모델-뷰-컨트롤러*합니다. MVC는 응용 프로그램을 설계, 테스트 및 유지 관리 하기 쉬운 개발을 위한 패턴입니다. MVC 기반 응용 프로그램에는 다음이 포함 되어 있습니다.

- **M** odels: 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하는 응용 프로그램의 데이터를 나타내는 클래스입니다.
- **V** iews: 응용 프로그램 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.
- **C** ontrollers: 들어오는 브라우저 요청을 처리 하는 클래스는 모델 데이터를 검색 하 고 브라우저에 대 한 응답을 반환 하는 템플릿 보기를 지정 합니다.

이 자습서 시리즈에서는 이러한 모든 개념을 다루는 수 하 고 응용 프로그램을 만들고 사용 하는 방법을 보여 됩니다.

> [!NOTE]
> 이전 단계의 기본 MVC 템플릿 선택 되었습니다. 이 만들어지고 홈 계정을 기본적으로 컨트롤러를 관리 합니다.

컨트롤러 클래스를 만들어 시작 해 보겠습니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더 및 클릭 한 다음 **추가**, 다음 **컨트롤러**합니다.


![](adding-a-controller/_static/image1.png)

에 **스 캐 폴드 추가** 대화 상자, 클릭 **MVC 5 컨트롤러-비어 있음**를 클릭 하 고 **추가**합니다.

![](adding-a-controller/_static/image2.png)  
 

새 컨트롤러 "HelloWorldController" 이름을 지정 하 고 클릭 **추가**합니다.

![컨트롤러 추가](adding-a-controller/_static/image3.png)

확인할 수 있습니다 **솔루션 탐색기** 새 파일이 만들어졌음을 명명 *HelloWorldController.cs* 하 고 새 폴더 *Views\HelloWorld*합니다. 컨트롤러는 IDE에서 열려 있습니다.

![](adding-a-controller/_static/image4.png)

파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

컨트롤러 메서드는 예를 들어 html 문자열을 반환 합니다. 컨트롤러 이름은 `HelloWorldController` 첫 번째 메서드는 이름이 `Index`합니다. 브라우저에서 호출 해 보겠습니다. (F5 또는 ctrl+f5를 누릅니다) 응용 프로그램을 실행 합니다. 브라우저에서 추가 &quot;HelloWorld&quot; 주소 표시줄의 경로에 있습니다. (그림의 아래에서 예를 들어 `http://localhost:1234/HelloWorld.`) 페이지를 브라우저에서 다음 스크린샷과 같이 표시 됩니다. 위의 메서드에 코드를 직접 문자열을 반환 합니다. 일부 HTML을 반환 하도록 시스템을 지시 및 못해서!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC는 들어오는 URL에 따라 다른 컨트롤러 클래스 (및 그 안에 다양 한 작업 메서드)를 호출합니다. ASP.NET MVC에서 사용 되는 기본 URL 라우팅 논리를 호출 하는 코드를 확인 하려면 다음과 같은 형식을 사용 합니다.

`/[Controller]/[ActionName]/[Parameters]`

라우팅에 대 한 형식으로 설정 합니다 *앱\_Start/RouteConfig.cs* 파일입니다.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

응용 프로그램을 실행 하 고 URL 세그먼트를 제공 하지 않는 경우 "Home" 컨트롤러에 기본적으로 및 "Index" 작업 메서드는 위의 코드의 기본값 섹션에서 지정 합니다.

URL의 첫 번째 부분 실행할 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 매핑되는 `HelloWorldController` 클래스입니다. URL의 두 번째 부분 클래스에 대 한 작업 메서드를 결정 합니다. 따라서 */HelloWorld/인덱스* 로 인해를 `Index` 메서드의 `HelloWorldController` 실행 하는 클래스입니다. 이동할 있었습니다 되었다는 */HelloWorld* 및 `Index` 메서드는 기본적으로 사용 되었습니다. 라는 메서드가 때문에 이것이 `Index` 명시적으로 지정 하지 않으면 컨트롤러에서 호출 되는 기본 방법입니다. URL 세그먼트(`Parameters`)의 세 번째 부분은 경로 데이터입니다. 이 자습서에서는 경로 데이터를 나중에 표시 됩니다 것입니다.

`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다. 합니다 `Welcome` 실행 하 고 문자열을 반환 &quot;이 시작 작업 메서드입니다... &quot;. 기본 MVC 매핑이 `/[Controller]/[ActionName]/[Parameters]`합니다. 이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.

![](adding-a-controller/_static/image6.png)

일부 매개 변수 정보를 URL에서 컨트롤러를 전달할 수 있도록 약간에서 예제를 보겠습니다 수정 (예를 들어 */HelloWorld/시작? name = Scott&amp;numtimes = 4*). 변경에 `Welcome` 아래와 같이 두 개의 매개 변수를 포함 하는 방법입니다. 코드를 나타내는 C# 선택적 매개 변수 기능을 사용 하는 참고를 `numTimes` 매개 변수는 기본적으로 1 값이 없는 매개 변수에 대해 전달 되 면 합니다.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> 보안 참고: 사용 하 여 위의 코드 [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) 악의적인 입력 (예: JavaScript)에서 응용 프로그램을 보호 합니다. 자세한 내용은 참조 [방법: 보호에 대 한 스크립트 악용 문자열을 HTML 인코딩 적용 하 여 웹 응용 프로그램에서](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)합니다.


 응용 프로그램을 실행 하 고 예제 URL로 이동 (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`). 다른 값을 사용할 수 있습니다 `name` 고 `numtimes` url에서입니다. 합니다 [ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 메서드에서 매개 변수로 주소 표시줄에는 쿼리 문자열에서 명명 된 매개 변수를 자동으로 매핑합니다.

![](adding-a-controller/_static/image7.png)

URL 세그먼트 위 샘플에서 ( `Parameters`)를 사용 하지 않으면 합니다 `name` 하 고 `numTimes` 매개 변수가 전달 [쿼리 문자열](http://en.wikipedia.org/wiki/Query_string)합니다. ? (물음표)는 구분 기호는 위 URL에서 및 쿼리 문자열이 이어집니다. &amp; 문자는 쿼리 문자열을 구분합니다.

시작 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

응용 프로그램을 실행 하 고 다음 URL을 입력 합니다. `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

이 이번 세 번째 URL 세그먼트 일치 경로 매개 변수 `ID.` 는 `Welcome` 매개 변수를 포함 하는 작업 메서드 (`ID`) URL 사양에서 일치 하는 `RegisterRoutes` 메서드.

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC 응용 프로그램의 것이 더 일반적 쿼리 문자열로 전달 보다 경로 데이터 (예: 위의 ID를 사용 하 여 했던)와 매개 변수를 전달 합니다. 모두 전달 하는 경로 추가할 수도 있습니다는 `name` 및 `numtimes` url에서 경로 데이터 매개 변수에서입니다. 에 *앱\_start\* 파일을 "Hello" 경로 추가 합니다.

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

응용 프로그램을 실행 하 고 이동 `/localhost:XXX/HelloWorld/Welcome/Scott/3`합니다.

![](adding-a-controller/_static/image9.png)

대부분의 MVC 응용 프로그램 기본 경로 제대로 작동합니다. 모델 바인더를 사용 하 여 데이터를 전달 하려면이 자습서의 뒷부분에 나오는 배웁니다 및에 대 한 기본 경로 수정할 필요가 없습니다.

이 예제에서 컨트롤러 작업을 수행 합니다 &quot;VC&quot; MVC 부분-즉, 뷰 및 컨트롤러 작업입니다. 컨트롤러 HTML을 직접 반환 됩니다. 일반적으로 컨트롤러 코드 번거로운 복잡해 지므로 HTML을 직접 반환 하지 않으려고 합니다. 대신 일반적으로 별도 뷰 템플릿 파일을 HTML 응답을 생성 하는 데 사용 됩니다. 어떻게이 위해서는 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started.md)
> [다음](adding-a-view.md)
