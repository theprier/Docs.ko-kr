---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 뷰 (C#) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 50ce4a2024ffd9e2bbb5526717052d486689ff38
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-view-c"></a>뷰 (C#) 추가
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


이 섹션에 수정 하려는 `HelloWorldController` 템플릿 파일을 명확 하 게 캡슐화 하는 프로세스를 클라이언트에 HTML 응답을 생성 하는 뷰를 사용 하는 클래스입니다.

사용 하 여 새 보기 템플릿 파일을 만듭니다 [Razor 뷰 엔진](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) ASP.NET MVC 3으로 도입 되었습니다. Razor 기반 보기 템플릿에 *.cshtml* 파일 확장명이 및 C#을 사용 하 여 출력 하는 HTML을 만들기 위해 세련 된 방법을 제공 합니다. Razor 뷰 템플릿을 작성할 때 필요한 키 입력 및 문자 수를 최소화 하 고 워크플로 코딩 빠르지 유체를 활성화 합니다.

있는 뷰 템플릿을 사용 하 여 시작 된 `Index` 에서 메서드는 `HelloWorldController` 클래스입니다. 현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다. 변경 된 `Index` 반환 하는 메서드는 `View` 다음과 같이 개체:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

이 코드는 템플릿 보기를 사용 하 여 브라우저에 HTML 응답을 생성 합니다. 프로젝트에서 사용할 수 있는 보기 템플릿을 추가 `Index` 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 `Index` 클릭 **뷰 추가**합니다.

![](adding-a-view/_static/image1.png)

**뷰 추가** 대화 상자가 나타납니다. 클릭 하는 방법은 기본값을 그대로 두고는 **추가** 단추:

![](adding-a-view/_static/image2.png)

*MvcMovie\Views\HelloWorld* 폴더 및 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 생성 됩니다. 한꺼번에 보일 **솔루션 탐색기**:

![](adding-a-view/_static/image3.png)

에서는 다음의 *Index.cshtml* 만들어진 파일:

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

일부 HTML에서 추가 된 `<h2>` 태그입니다. 수정 된 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

응용 프로그램을 실행 하 고를 찾습니다는 `HelloWorld` 컨트롤러 (`http://localhost:xxxx/HelloWorld`). `Index` 메서드 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`, 메서드가 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿 파일을 사용 하도록 지정 합니다. ASP.NET MVC를 사용 하 여 기본값으로 사용할 보기 템플릿 파일의 이름을 명시적으로 지정 하지 않은, 때문에 *Index.cshtml* 에서 파일 보기는 *\Views\HelloWorld* 폴더입니다. 아래 이미지 보기에 하드 코드 된 문자열을 보여 줍니다.

![](adding-a-view/_static/image6.png)

잘 보입니다. 그러나 고 해당 데이터베이스는 브라우저의 제목 표시줄 표시 "Index" 페이지에서 큰 제목에 "내 MVC 응용 프로그램입니다." 라고 표시 이러한 변경 해보겠습니다.

## <a name="changing-views-and-layout-pages"></a>레이아웃 페이지 및 뷰 변경

첫째, 페이지의 위쪽 "내 MVC 응용 프로그램" 제목을 변경 하려면. 텍스트를 모든 페이지에 공통적으로 적용 합니다. 실제로 것이 프로젝트에만 한 곳에서 응용 프로그램에서 모든 페이지에 표시 되지만 더 합니다. 이동 하는 */뷰/공유* 폴더에 **솔루션 탐색기** 엽니다는  *\_Layout.cshtml* 파일입니다. 이 파일은 라고는 *레이아웃 페이지* 공유 "셸" 다른 모든 페이지를 사용 하는 것이 고 합니다.

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

레이아웃 서식 파일을 사용 하면 한 곳에서 사이트의 HTML 컨테이너 레이아웃을 지정 하 고 다음 사이트에서 여러 페이지에 걸쳐 적용 수 있도록 합니다. 참고는 `@RenderBody()` 파일의 맨 아래 근처의 줄 합니다. `RenderBody` 여기서 만드는 모든 보기 전용 페이지 표시, "래핑된" 레이아웃 페이지의 자리 표시자가입니다. 제목 제목에 "내 MVC 응용 프로그램에서" "MVC 만든 동영상 앱"의 레이아웃 템플릿 변경 합니다.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

응용 프로그램을 실행 하 고 "MVC 영화 App"는 이제 표시. 클릭는 **에 대 한** 어떻게 해당 페이지에 표시 "MVC 영화 App" 너무 참조 링크를 지정 하 고 있습니다. 레이아웃 템플릿을 한 번 변경 사항을 적용할 수 있었습니다 하 고 사이트에 있는 모든 페이지에 새 제목의 반영 합니다.

![](adding-a-view/_static/image9.png)

전체  *\_Layout.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

이제 인덱스 페이지 (뷰)의 제목을 변경 해보겠습니다.

Open *MvcMovie\Views\HelloWorld\Index.cshtml*. 변경 하는 두 곳: 먼저 텍스트 표시 되는 브라우저의 제목에 찾은 다음 보조 헤더에서 (의 `<h2>` 요소). 어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

나타내는 집합 위의 코드를 표시 하려면 HTML 제목은 `Title` 의 속성은 `ViewBag` 개체 (에 *Index.cshtml* 템플릿 보기). 레이아웃 서식 파일의 소스 코드를 다시 확인 하는 경우 서식 파일에서이 값을 사용을 확인할 수 있습니다는 `<title>` 의 일환으로 요소는 `<head>` HTML의 섹션입니다. 이 방법을 사용 하는 보기 템플릿과 레이아웃 파일 간의 다른 매개 변수를 쉽게 전달할 수 있습니다.

응용 프로그램을 실행 하 고 찾아보기 `http://localhost:xx/HelloWorld`합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.)

또한 방법을의 콘텐츠는 *Index.cshtml* 템플릿 보기 병합 된는  *\_Layout.cshtml* 템플릿 보기와 하나의 HTML 응답을 브라우저에 보냈습니다. 레이아웃 템플릿을 사용하면 응용 프로그램의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.

![](adding-a-view/_static/image10.png)

그렇지만 일부 “데이터”(이 경우 “Hello from our View Template!” 메시지)는 하드 코드되었습니다. MVC 응용 프로그램에는 "V"(보기)가 있으며 "C"(컨트롤러)가 있지만 "M"(모델)은 아직 없습니다. 곧 살펴봅니다 방법 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

데이터베이스를 이동 하 고 모델에 대해 설명 하는, 하지만 먼저에 대해 살펴보기 보기에는 컨트롤러에서 정보를 전달 합니다. 컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다. 컨트롤러 클래스는 들어오는 매개 변수를 처리, 데이터베이스에서 데이터를 검색 하 고 브라우저에 다시 전송할 응답의 유형을 결정 하는 코드를 작성할 위치입니다. 템플릿 보기를 생성 하 고 브라우저에 대 한 HTML 응답 형식을 지정 하는 컨트롤러에서 사용할 수 있습니다.

컨트롤러는 모든 데이터 나 개체 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿에 대 한 순서에 필요한 제공 해야 합니다. 템플릿 보기는 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 하지 해야 합니다. 컨트롤러를 제공 하는 데이터와만 작동 해야 합니다. 이 "문제의 분리" 유지 관리 하 고 더 쉽게 유지 관리할 코드를 유지할 수 있습니다.

현재는 `Welcome` 의 동작 메서드에 `HelloWorldController` 걸립니다 클래스는 `name` 및 `numTimes` 매개 변수 및 브라우저에 직접 값을 출력 합니다. 이 응답을 문자열로 렌더링 되는 컨트롤러를 갖는 대신 보기 서식 파일을 대신 사용 하는 컨트롤러를 변경해 보겠습니다. 보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다. 컨트롤러 템플릿 보기에는 동적 데이터를 저장 하 여이 수행할 수는 `ViewBag` 템플릿 보기에 액세스할 수 있는 개체입니다.

돌아가서는 *HelloWorldController.cs* 파일을 변경는 `Welcome` 를 추가 하려면 메서드는 `Message` 및 `NumTimes` 값을 `ViewBag` 개체입니다. `ViewBag` 넣을 수 있습니다에 원하는 것을 의미 하는 동적 개체 `ViewBag` 내부 요소를 넣으면 될 때까지 개체에 정의 된 속성이 없습니다. 전체 *HelloWorldController.cs* 파일은 다음과 같습니다.

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

이제는 `ViewBag` 개체가 자동으로 보기에 전달 되는 데이터를 포함 합니다.

다음으로 시작 뷰 서식 파일이 필요 있습니다! 에 **디버그** 메뉴 선택 **MvcMovie 빌드** 프로젝트가 컴파일될 되도록 합니다.

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

그런 다음 마우스 오른쪽 단추로 클릭는 `Welcome` 클릭 **뷰 추가**합니다. 같습니다는 **뷰 추가** 같은 대화 상자가 나타납니다.

![](adding-a-view/_static/image13.png)

클릭 **추가**, 아래에서 다음 코드를 추가 하 고는 `<h2>` 새로운 요소 *Welcome.cshtml* 파일입니다. 사용자가 예상 횟수 만큼 "Hello" 라고 표시 하는 루프를 만들어야 합니다. 전체 *Welcome.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

이제 데이터 URL에서 수행 되 고 컨트롤러에 자동으로 전달 합니다. 컨트롤러에 데이터를 패키지 한 `ViewBag` 개체 및 보기에 해당 개체를 전달 합니다. 뷰는 다음 사용자에 게 HTML로 데이터를 표시합니다.

![](adding-a-view/_static/image14.png)

이는 모델에 대한 일종의 "M"이었지만 데이터베이스 종류는 아니었습니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
