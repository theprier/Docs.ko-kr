---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 추가 보기 (C#) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: e9496f801024bd2d4a135eefbb79b162017197b7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366218"
---
<a name="adding-a-view-c"></a>추가 보기 (C#)
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


이 섹션에서 수정 하려는 `HelloWorldController` 명확 하 게 템플릿 파일을 클라이언트에 대 한 HTML 응답을 생성 하는 과정을 캡슐화 하는 뷰를 사용 하는 클래스입니다.

새 뷰 템플릿 파일을 만듭니다 [Razor 보기 엔진](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) ASP.NET MVC 3으로 도입 되었습니다. Razor 기반 뷰 템플릿에 *.cshtml* 파일 확장명 및 C#을 사용 하 여 출력 HTML 만드는 세련 된 방법을 제공 합니다. Razor는 뷰 템플릿을 작성 하는 데 필요한 키 입력 및 문자 수를 최소화 하 고 워크플로 코딩 하는 빠르고, 유체를 활성화 합니다.

사용 하 여 보기 템플릿을 사용 하 여 시작 합니다 `Index` 의 메서드는 `HelloWorldController` 클래스. 현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다. 변경 합니다 `Index` 반환할 메서드를 `View` 개체를 다음에 표시 된 대로:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

이 코드는 브라우저에 HTML 응답을 생성 하려면 보기 템플릿을 사용 합니다. 프로젝트에서 사용 하 여 사용할 수 있는 보기 템플릿을 추가 합니다 `Index` 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 `Index` 메서드와 클릭 **뷰 추가**합니다.

![](adding-a-view/_static/image1.png)

합니다 **뷰 추가** 대화 상자가 나타납니다. 기본값을 클릭 하는 방법은 그대로 합니다 **추가** 단추:

![](adding-a-view/_static/image2.png)

합니다 *MvcMovie\Views\HelloWorld* 폴더와 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 생성 됩니다. 볼 수 있습니다 **솔루션 탐색기**:

![](adding-a-view/_static/image3.png)

다음은 *Index.cshtml* 생성 된 파일:

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

아래 일부 HTML을 추가 합니다 `<h2>` 태그입니다. 수정 된 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

응용 프로그램을 실행 하 고 이동 합니다 `HelloWorld` 컨트롤러 (`http://localhost:xxxx/HelloWorld`). 합니다 `Index` 메서드를 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`, 메서드 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿 파일을 사용 해야 함을 지정 하는 합니다. ASP.NET MVC를 사용 하 여 기본값으로 사용 하 여 뷰 템플릿 파일의 이름을 명시적으로 지정 하지, 때문에 합니다 *Index.cshtml* 보기 파일을 *\Views\HelloWorld* 폴더입니다. 아래 이미지는 보기에서 하드 코드 된 문자열을 보여 줍니다.

![](adding-a-view/_static/image6.png)

잘 찾습니다. 그러나 브라우저의 제목 표시줄 "Index" 라는 페이지의 큰 제목에 "내 MVC 응용 프로그램입니다." 라는 것을 알합니다 이러한 파일을 변경해 보겠습니다.

## <a name="changing-views-and-layout-pages"></a>보기 및 레이아웃 페이지 변경

먼저, 페이지의 맨 위에 있는 "내 MVC 응용 프로그램" title을 변경 하려고 합니다. 텍스트를 모든 페이지에 공통적으로 적용 합니다. 실제로 구현 프로젝트에만 한 곳에서 응용 프로그램에서 모든 페이지에 나타나는 경우에 합니다. 로 이동 합니다 */뷰/공유* 폴더에 **솔루션 탐색기** 연 합니다  *\_Layout.cshtml* 파일입니다. 이 파일은 호출을 *레이아웃 페이지* 공유 "셸" 다른 모든 페이지를 사용 하는 것입니다.

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

레이아웃 템플릿을 한 곳에서 사이트의 HTML 컨테이너 레이아웃을 지정 하 고 다음 사이트에서 여러 페이지에 걸쳐 적용할 수 있습니다. 참고는 `@RenderBody()` 파일의 아래쪽에 있는 줄. `RenderBody` 여기서 만든 모든 보기 전용 페이지가 표시, 레이아웃 페이지에서 "래핑된" 자리 표시자가입니다. 레이아웃 템플릿에서 "내 MVC 응용 프로그램"을 "MVC 동영상 앱"에서 제목 머리글을 변경 합니다.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

응용 프로그램을 실행 하 고 이제 "MVC 동영상 앱" 표시 되는 확인 합니다. 클릭 합니다 **에 대 한** 링크 하는 페이지 표시 되는 방식을 "MVC 동영상 앱"을 너무 참조 하세요. 레이아웃 템플릿에서 변경을 한 번 수행할 수 있었습니다 하 고 사이트의 모든 페이지에 새 제목의 반영 합니다.

![](adding-a-view/_static/image9.png)

전체  *\_Layout.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

이제 인덱스 페이지 (뷰)의 title을 변경해 보겠습니다.

오픈 *MvcMovie\Views\HelloWorld\Index.cshtml*합니다. 변경 하는 두 군데: 먼저 텍스트가 표시 되는 브라우저의 제목을 선택한 후 보조 헤더 (의 `<h2>` 요소). 어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

집합 위의 코드를 표시 하려면 HTML 제목을 나타내기 위해를 `Title` 의 속성을 `ViewBag` 개체 (보기로 제공 되는 *Index.cshtml* 템플릿 보기). 레이아웃 템플릿의 소스 코드를 다시 살펴보면 보면 템플릿에이 값을 `<title>` 요소의 일부로 `<head>` HTML 부분입니다. 이 방법을 사용 하는 뷰 템플릿 및 레이아웃 파일 간에 다른 매개 변수를 쉽게 전달할 수 있습니다.

응용 프로그램을 실행 하 고 이동 `http://localhost:xx/HelloWorld`합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.)

또한 하는 방법을 콘텐츠를 *Index.cshtml* 보기 템플릿을 사용 하 여 병합 된를  *\_Layout.cshtml* 템플릿 보기 및 단일 HTML 응답이 브라우저로 전송 되었습니다. 레이아웃 템플릿을 사용하면 응용 프로그램의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.

![](adding-a-view/_static/image10.png)

그렇지만 일부 “데이터”(이 경우 “Hello from our View Template!” 메시지)는 하드 코드되었습니다. MVC 응용 프로그램에는 "V"(보기)가 있으며 "C"(컨트롤러)가 있지만 "M"(모델)은 아직 없습니다. 잠시 후 살펴보겠습니다 방법을 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

전에 데이터베이스로 이동 하 고 모델에 대 한 설명, 그러나 처음에 대해 살펴보겠습니다 정보를 컨트롤러에서 보기로 전달 합니다. 컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다. 컨트롤러 클래스는, 들어오는 매개 변수를 처리 하 고, 데이터베이스에서 데이터를 검색 하 고, 궁극적으로 브라우저에 다시 전송할 응답의 유형을 결정 하는 코드를 작성 하는 위치입니다. 템플릿 보기 생성 하 고 브라우저에 HTML 응답을 형식 컨트롤러에서 사용할 수 있습니다.

컨트롤러는 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿은 순서에 필요한 모든 데이터 또는 개체를 제공 하는 일을 담당 합니다. 보기 템플릿에서 되지 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 해야 합니다. 대신, 컨트롤러에서 제공 되는 데이터와만 작동 해야 합니다. 이 "문제의 분리"를 유지 관리 정리 하 고 유지 관리 코드를 유지할 수 있습니다.

현재는 `Welcome` 에서 작업 메서드는 `HelloWorldController` 클래스를 `name` 및 `numTimes` 매개 변수 및 브라우저에 직접 값을 출력 합니다. 문자열로이 응답을 렌더링 하는 컨트롤러를 갖는 대신 보기 템플릿을 대신 사용 하는 컨트롤러를 변경해 보겠습니다. 보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다. 컨트롤러에서 템플릿 보기에는 동적 데이터를 배치 함으로써이 수행할 수는 `ViewBag` 개체 보기 템플릿에서 액세스할 수 있도록 합니다.

돌아갑니다를 *HelloWorldController.cs* 파일을 변경 합니다 `Welcome` 메서드를 추가 `Message` 및 `NumTimes` 값을 `ViewBag` 개체. `ViewBag` 넣으면에 원하는 것을 의미 하는 동적 개체 `ViewBag` 내부에 무언가 배치 될 때까지 개체에 정의 된 속성이 없습니다. 전체 *HelloWorldController.cs* 파일은 다음과 같습니다.

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

이제는 `ViewBag` 보기로 자동으로 전달 되는 데이터를 포함 하는 개체입니다.

다음으로 시작 보기 템플릿을 해야! 에 **디버그** 메뉴에서 **빌드 MvcMovie** 프로젝트 컴파일 되었는지 확인 하려면.

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

내에서 마우스 오른쪽 단추로 클릭 합니다 `Welcome` 메서드와 클릭 **뷰 추가**합니다. 같습니다 합니다 **뷰 추가** 같은 대화 상자가 나타납니다.

![](adding-a-view/_static/image13.png)

클릭 **추가**, 한 다음 아래에 다음 코드를 추가 합니다 `<h2>` 새 요소 *Welcome.cshtml* 파일. 사용자가 예상 만큼 "Hello"를 표시 하는 루프를 만들어야 합니다. 전체 *Welcome.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

이제 데이터 URL에서 가져온 것 이며 자동으로 컨트롤러에 전달 됩니다. 에 데이터를 패키지 하는 컨트롤러를 `ViewBag` 개체와 뷰에 해당 개체를 전달 합니다. 뷰는 다음 사용자에 게 HTML로 데이터를 표시합니다.

![](adding-a-view/_static/image14.png)

이는 모델에 대한 일종의 "M"이었지만 데이터베이스 종류는 아니었습니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
