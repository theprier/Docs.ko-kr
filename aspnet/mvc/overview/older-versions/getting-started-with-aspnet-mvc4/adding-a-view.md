---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 뷰 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 6244bfd96c547c5ccbcaed7ba17214df49d2886c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829387"
---
<a name="adding-a-view"></a>뷰 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.


이 섹션에서 수정 하려는 `HelloWorldController` 명확 하 게 템플릿 파일을 클라이언트에 대 한 HTML 응답을 생성 하는 과정을 캡슐화 하는 뷰를 사용 하는 클래스입니다.

사용 하 여 뷰 템플릿 파일을 만들어야 합니다 [Razor 보기 엔진](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) ASP.NET MVC 3으로 도입 되었습니다. Razor 기반 뷰 템플릿에 *.cshtml* 파일 확장명 및 C#을 사용 하 여 출력 HTML 만드는 세련 된 방법을 제공 합니다. Razor는 뷰 템플릿을 작성 하는 데 필요한 키 입력 및 문자 수를 최소화 하 고 워크플로 코딩 하는 빠르고, 유체를 활성화 합니다.

현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다. 변경 합니다 `Index` 반환할 메서드를 `View` 다음 코드 에서처럼 개체:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

`Index` 위의 메서드는 뷰 템플릿을 사용 하 여 브라우저에 HTML 응답을 생성 합니다. 컨트롤러 메서드 (라고도 [작업 메서드에](http://rachelappel.com/asp.net-mvc-actionresults-explained)), 같은 합니다 `Index` 메서드 위의 일반적으로 반환를 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (에서 파생 된 클래스 또는 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), 문자열 같은 기본 형식이 아닌 합니다.

프로젝트에서 사용 하 여 사용할 수 있는 보기 템플릿을 추가 합니다 `Index` 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 `Index` 메서드와 클릭 **뷰 추가**합니다.

![](adding-a-view/_static/image1.png)

합니다 **뷰 추가** 대화 상자가 나타납니다. 기본값을 클릭 하는 방법은 그대로 합니다 **추가** 단추:

![](adding-a-view/_static/image2.png)

합니다 *MvcMovie\Views\HelloWorld* 폴더와 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 생성 됩니다. 볼 수 있습니다 **솔루션 탐색기**:

![](adding-a-view/_static/image3.png)

다음은 *Index.cshtml* 생성 된 파일:

![HelloWorldIndex](adding-a-view/_static/image4.png)

아래에 있는 다음 HTML을 추가 합니다 `<h2>` 태그입니다.

[!code-html[Main](adding-a-view/samples/sample2.html)]

전체 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

Visual Studio 2012, 솔루션 탐색기를 사용 하는 경우 마우스 오른쪽 단추로 클릭 합니다 *Index.cshtml* 파일을 선택 **페이지 검사기에서 보기**합니다.

![PI](adding-a-view/_static/image5.png)

합니다 [페이지 검사기 자습서](../../views/using-page-inspector-in-aspnet-mvc.md) 이 새 도구에 대 한 자세한 정보가 있습니다.

또는 응용 프로그램을 실행 하 고 이동 합니다 `HelloWorld` 컨트롤러 (`http://localhost:xxxx/HelloWorld`). 합니다 `Index` 메서드를 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`, 메서드 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿 파일을 사용 해야 함을 지정 하는 합니다. ASP.NET MVC를 사용 하 여 기본값으로 사용 하 여 뷰 템플릿 파일의 이름을 명시적으로 지정 하지, 때문에 합니다 *Index.cshtml* 보기 파일을 *\Views\HelloWorld* 폴더입니다. 아래 이미지는 문자열을 보여 줍니다 &quot;Hello from our View Template!&quot; 보기에서 하드 코딩 합니다.

![](adding-a-view/_static/image6.png)

잘 찾습니다. 그러나 브라우저의 제목 표시줄에 표시 되는지 확인할 수 있습니다 &quot;내 ASP.NET는 인덱스&quot; 라는 페이지 맨 위에 있는 큰 링크 및 &quot;사용자 로고는 여기 있습니다.&quot; 아래는 &quot;에 로고.&quot; 되며 등록 홈에 대 한 링크는 아래 링크에 로그 정보 및 연락처 페이지를 링크 합니다. 그 중 일부를 변경해 보겠습니다.

## <a name="changing-views-and-layout-pages"></a>보기 및 레이아웃 페이지 변경

변경 하려면 먼저 합니다 &quot;에 로고.&quot; 페이지의 맨 위에 있는 제목입니다. 텍스트를 모든 페이지에 공통적으로 적용 합니다. 응용 프로그램에서 모든 페이지에 표시 되더라도 실제로 프로젝트에만 한 곳에서 구현 됩니다. 로 이동 합니다 */뷰/공유* 폴더에 **솔루션 탐색기** 연 합니다  *\_Layout.cshtml* 파일입니다. 이 파일은 호출을 *레이아웃 페이지* 공유 되며 &quot;셸&quot; 다른 모든 페이지를 사용 하는 합니다.

![_LayoutCshtml](adding-a-view/_static/image7.png)

레이아웃 템플릿을 한 곳에서 사이트의 HTML 컨테이너 레이아웃을 지정 하 고 다음 사이트에서 여러 페이지에 걸쳐 적용할 수 있습니다. `@RenderBody()` 줄을 찾습니다. `RenderBody`는 사용자가 만드는 모든 보기 전용 페이지가 표시되는 자리 표시자이며 레이아웃 페이지에서 &quot;래핑됩니다&quot;. 예를 들어, 정보 링크를 선택 하는 경우는 *Views\Home\About.cshtml* 보기 내에서 렌더링 되는 `RenderBody` 메서드.

사이트 제목 머리글에서 레이아웃 템플릿에 변경 &quot;여기에 로고&quot; 하 &quot;MVC 동영상&quot;합니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

제목 요소의 콘텐츠를 다음 태그로 바꿉니다.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

응용 프로그램을 이제 다음과 같은 알림이 실행 &quot;MVC Movie &quot;합니다. 클릭 합니다 **에 대 한** 링크 하는 페이지에 표시 하는 방법을 참조 하세요 &quot;MVC 동영상&quot;도 합니다. 레이아웃 템플릿에서 변경을 한 번 수행할 수 있었습니다 하 고 사이트의 모든 페이지에 새 제목의 반영 합니다.

![](adding-a-view/_static/image8.png)

이제 인덱스 뷰의 제목을 변경해 보겠습니다.

오픈 *MvcMovie\Views\HelloWorld\Index.cshtml*합니다. 변경 하는 두 군데: 먼저 텍스트가 표시 되는 브라우저의 제목을 선택한 후 보조 헤더 (의 `<h2>` 요소). 어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

집합 위의 코드를 표시 하려면 HTML 제목을 나타내기 위해를 `Title` 의 속성을 `ViewBag` 개체 (보기로 제공 되는 *Index.cshtml* 템플릿 보기). 레이아웃 템플릿의 소스 코드를 다시 살펴보면 보면 템플릿에이 값은 `<title>` 요소의 일부로 `<head>` 이전에 수정한는 HTML 부분입니다. 이 사용 하 여 `ViewBag` 방법을 쉽게 전달할 수 다른 매개 변수 보기 템플릿에 사이의 레이아웃 파일입니다.

응용 프로그램을 실행 하 고 이동 `http://localhost:xx/HelloWorld`합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.) 브라우저 제목으로 생성 됩니다는 `ViewBag.Title` 에서 설정 합니다 *Index.cshtml* 템플릿 및 추가 보기 &quot;-동영상 앱&quot; 레이아웃 파일에 추가 합니다.

또한 하는 방법을 콘텐츠를 *Index.cshtml* 보기 템플릿을 사용 하 여 병합 된를  *\_Layout.cshtml* 템플릿 보기 및 단일 HTML 응답이 브라우저로 전송 되었습니다. 레이아웃 템플릿을 사용하면 응용 프로그램의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.

![](adding-a-view/_static/image9.png)

우리의 약간의 &quot;데이터&quot; (이 경우에 &quot;Hello from our View Template!&quot; 메시지) 그러나 하드 코드 됩니다. MVC 응용 프로그램에는 &quot;V&quot; (뷰)가 있으며를 &quot;C&quot; (컨트롤러)가 없는 &quot;M&quot; (모델) 아직 합니다. 잠시 후 살펴보겠습니다 방법을 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

전에 데이터베이스로 이동 하 고 모델에 대 한 설명, 그러나 처음에 대해 살펴보겠습니다 정보를 컨트롤러에서 보기로 전달 합니다. 컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다. 컨트롤러 클래스를 작성 하는 위치는 들어오는 브라우저를 처리 하는 코드 요청 데이터베이스에서 데이터를 검색 하 고 궁극적으로 브라우저에 다시 전송할 응답의 유형을 결정 합니다. 템플릿 보기 생성 하 고 브라우저에 HTML 응답을 형식 컨트롤러에서 사용할 수 있습니다.

컨트롤러는 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿은 순서에 필요한 모든 데이터 또는 개체를 제공 하는 일을 담당 합니다. 모범 사례: **보기 템플릿에서 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 하지 해야**합니다. 대신 보기 템플릿을 컨트롤러에서 제공 되는 데이터와만 작동 해야 합니다. 이 유지 관리 &quot;중요 한 부분의 분리&quot; 상태를 유지할 수 코드 정리, 테스트 및 유지 관리가 더 쉬워집니다.

현재는 `Welcome` 에서 작업 메서드는 `HelloWorldController` 클래스를 `name` 및 `numTimes` 매개 변수 및 브라우저에 직접 값을 출력 합니다. 문자열로이 응답을 렌더링 하는 컨트롤러를 갖는 대신 보기 템플릿을 대신 사용 하는 컨트롤러를 변경해 보겠습니다. 보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다. 컨트롤러에서 템플릿 보기에는 동적 데이터 (매개 변수)를 배치 함으로써이 수행할 수는 `ViewBag` 개체 보기 템플릿에서 액세스할 수 있도록 합니다.

돌아갑니다를 *HelloWorldController.cs* 파일을 변경 합니다 `Welcome` 메서드를 추가 `Message` 및 `NumTimes` 값을 `ViewBag` 개체. `ViewBag` 넣으면에 원하는 것을 의미 하는 동적 개체 `ViewBag` 내부에 무언가 배치 될 때까지 개체에 정의 된 속성이 없습니다. [ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 명명 된 매개 변수를 자동으로 매핑합니다 (`name` 및 `numTimes`)에서 메서드의 매개 변수로 주소 표시줄의 쿼리 문자열입니다. 전체 *HelloWorldController.cs* 파일은 다음과 같습니다.

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

이제는 `ViewBag` 보기로 자동으로 전달 되는 데이터를 포함 하는 개체입니다.

다음으로 시작 보기 템플릿을 해야! 에 **빌드** 메뉴에서 **빌드 MvcMovie** 프로젝트 컴파일 되었는지 확인 하려면.

내에서 마우스 오른쪽 단추로 클릭 합니다 `Welcome` 메서드와 클릭 **뷰 추가**합니다.

![](adding-a-view/_static/image10.png)

같습니다 합니다 **뷰 추가** 같은 대화 상자가 나타납니다.

![](adding-a-view/_static/image11.png)

클릭 **추가**, 한 다음 아래에 다음 코드를 추가 합니다 `<h2>` 새 요소 *Welcome.cshtml* 파일. 라고 표시 하는 루프를 만듭니다 &quot;Hello&quot; 만큼 많은 사용자가 해야 합니다. 전체 *Welcome.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

데이터는 URL에서 수행 하 고 사용 하 여 컨트롤러에 전달 하는 이제 합니다 [바인더 모델](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)합니다. 에 데이터를 패키지 하는 컨트롤러를 `ViewBag` 개체와 뷰에 해당 개체를 전달 합니다. 뷰는 다음 사용자에 게 HTML로 데이터를 표시합니다.

![](adding-a-view/_static/image12.png)

위의 샘플에서는 사용 된 `ViewBag` 컨트롤러에서 보기로 데이터를 전달 하는 개체입니다. 자습서의 두 번째에서는 모델을 사용 뷰 컨트롤러에서 보기로 데이터를 전달 하 합니다. 뷰 모음 접근 방식을 통해 데이터를 전달 하는 보기 모델 방법은 일반적으로 훨씬 많이 사용 된 경우 블로그 항목을 참조 하세요 [동적 V 강력한 형식의 뷰](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 자세한 내용은 합니다.

저장소를 일종의 &quot;M&quot; 모델 이지만 데이터베이스 유형은 하지에 대 한 합니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
