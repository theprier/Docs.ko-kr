---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 뷰 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: cbb1b9572c1b1eb671eb2756b5920dc823963e8c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828657"
---
<a name="adding-a-view-vb"></a>뷰 (VB) 추가
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/adding-a-view.md) 이 자습서의 합니다.


이 섹션을 수정 하려고 합니다 `HelloWorldController` 명확 하 게 보기 템플릿 파일을 사용 하는 클래스를 클라이언트에 대 한 HTML 응답을 생성 하는 과정을 캡슐화 합니다.

사용 하 여 보기 템플릿을 사용 하 여 시작 해 보겠습니다 합니다 `Index` 의 메서드는 `HelloWorldController` 클래스. 현재는 `Index` 메서드는 컨트롤러 클래스 내에 하드 코딩 된 메시지를 사용 하 여 문자열을 반환 합니다. 변경 합니다 `Index` 반환할 메서드를 `View` 개체를 다음에 표시 된 대로:

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

이제 추가해보겠습니다 보기 템플릿을 사용 하 여 호출할 수 있습니다 하는 프로젝트에는 `Index` 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 `Index` 메서드와 클릭 **뷰 추가**합니다.

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

합니다 **뷰 추가** 대화 상자가 나타납니다. 기본 항목을 그대로 두고을 클릭 합니다 **추가** 단추입니다.

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

합니다 *MvcMovie\Views\HelloWorld* 폴더와 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일이 생성 됩니다. 볼 수 있습니다 **솔루션 탐색기**:

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

아래 일부 HTML을 추가 합니다 `<h2>` 태그입니다. 수정 된 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일은 다음과 같습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

응용 프로그램을 실행 하 고 이동 합니다 &quot;hello world&quot; 컨트롤러 (`http://localhost:xxxx/HelloWorld`). `Index` 메서드를 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`는 표시 된 보기 템플릿 파일을 사용 하 여 클라이언트에 대 한 응답을 렌더링 하려고 했습니다. ASP.NET MVC를 사용 하 여 기본값으로에서는 않았습니다 지정 하지 않으므로 명시적으로 사용 하 여 뷰 템플릿 파일의 이름, 합니다 *Index.vbhtml* 내에서 파일 보기는 *\Views\HelloWorld* 폴더입니다. 아래 이미지는 보기에서 하드 코드 된 문자열을 보여 줍니다.

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

잘 찾습니다. 그러나 브라우저의 제목 표시줄에 표시 됩니다는 것을 알 &quot;인덱스&quot; 페이지에서 큰 제목과 고 &quot;내 MVC 응용 프로그램입니다.&quot; 이러한 파일을 변경해 보겠습니다.

## <a name="changing-views-and-layout-pages"></a>보기 및 레이아웃 페이지 변경

먼저 텍스트를 변경해 보겠습니다 &quot;내 MVC 응용 프로그램입니다.&quot; 해당 텍스트를 공유 하 고 모든 페이지에 표시 됩니다. 실제로 나타나는 곳만 샘플 프로젝트의 경우 응용 프로그램에서 모든 페이지에도 합니다. 로 이동 합니다 */뷰/공유* 폴더에 **솔루션 탐색기** 연 합니다  *\_Layout.vbhtml* 파일입니다. 이 파일은 레이아웃 페이지 라고 이므로 공유 &quot;shell&quot; 다른 모든 페이지를 사용 하는 합니다.

참고는 `@RenderBody()` 파일의 아래쪽에 있는 코드 줄. `RenderBody` 만든 모든 페이지를 표시 하는 여기서 자리 표시자 &quot;래핑된&quot; 레이아웃 페이지에 있습니다. 변경 된 `<h1>` 에서 제목 **&quot;** 내 MVC 응용 프로그램&quot; 하 &quot;MVC 동영상 앱&quot;합니다.

[!code-html[Main](adding-a-view/samples/sample3.html)]

응용 프로그램을 실행 하 고 이제 라는 점에 유의 &quot;MVC 동영상 앱&quot;합니다. 클릭 합니다 **에 대 한** 하 고 링크를 표시 페이지 &quot;MVC 동영상 앱&quot;도 합니다.

전체  *\_Layout.vbhtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

이제 인덱스 페이지 (뷰)의 title을 변경해 보겠습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

오픈 *MvcMovie\Views\HelloWorld\Index.vbhtml*합니다. 변경 하는 두 군데: 먼저 텍스트가 표시 되는 브라우저의 제목을 선택한 후 보조 헤더 (의 `<h2>` 요소). 에서는 수 있도록 약간 다른 앱의 어느 부분을 변경 하는 약간의 코드를 볼 수 있습니다.

응용 프로그램을 실행 하 고 이동`http://localhost:xx/HelloWorld`합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. 큰 변경 하려면 약간 변경을 사용 하 여 응용 프로그램에서 뷰를 두는 것이 쉽습니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.)

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

우리의 약간의 &quot;데이터&quot; (이 경우에 &quot;Hello World!&quot; 메시지) 그러나 하드 코드 됩니다. MVC 응용 프로그램에 V (뷰) 및 C (컨트롤러) 하지만 없습니다 M (모델) 아직 준비 합니다. 잠시 후 살펴보겠습니다 방법을 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

전에 데이터베이스로 이동 하 고 모델에 대 한 설명, 그러나 처음에 대해 살펴보겠습니다 정보를 컨트롤러에서 보기로 전달 합니다. 클라이언트에 HTML 응답을 렌더링 하기 위해 필요한 사항 보기 템플릿을 전달 하려고 합니다. 보기 템플릿은 필요한 데이터만 포함 해야 하 고 이러한 개체는 일반적으로 만들고 템플릿 보기, 컨트롤러 클래스에 의해 전달-및 더 합니다.

사용 하 여 이전에 `HelloWorldController` 클래스를 `Welcome` 동작 메서드가 수행한를 `name` 및 `numTimes` 매개 변수 및 매개 변수 값은 브라우저에 다음 출력 합니다. 대신 계속 직접이 응답을 렌더링 하는 컨트롤러가 보다 보겠습니다 대신 넣습니다 데이터를 비닐 백에 포장에서 뷰에 대 한 합니다. 컨트롤러 및 뷰를 사용할 수는 `ViewBag` 해당 데이터를 보관 하는 개체입니다. 보기 템플릿에 자동으로 가리킬 되며 데이터로 모음의 콘텐츠를 사용 하 여 HTML 응답을 렌더링 하는 데 사용 합니다. 이런 방식으로 것과 다른 보기 템플릿은 컨트롤러 관련이-정리 유지 관리를 사용 하도록 설정 &quot;중요 한 부분의 분리&quot; 응용 프로그램 내에서.

또는 수 사용자 지정 클래스를 정의 다음 자체에서 해당 개체의 인스턴스를 생성, 데이터로 채울 하 고 보기에 전달 합니다. 라고를 ViewModel에 뷰에 대 한 사용자 지정 모델 이기 때문입니다. 그러나 데이터 양이 적고, ViewBag 잘 작동 합니다.

반환 합니다 *HelloWorldController.vb* 파일이 변경은 `Welcome` ViewBag 메시지 및 NumTimes 넣을 컨트롤러 내에서 메서드. ViewBag 동적 개체입니다. 즉, 원하는를 넣을 수 있습니다. 내부에 무언가 배치 될 때까지 ViewBag에 정의 된 속성이 없습니다.

전체 `HelloWorldController.vb` 동일한 파일에서 새 클래스를 사용 하 여 합니다.

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

이제 당사의 ViewBag 전달 되는 보기로 자동으로 데이터를 포함 합니다. 마찬가지로 또는 수 전달 했으므로 다음과 같이 고유한 개체에 우리가 원하는 경우:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

이제 해야는 `WelcomeView` 템플릿! 새 코드를 컴파일할 응용 프로그램을 실행 합니다. 브라우저를 닫고, 마우스 오른쪽 단추로 클릭 합니다 `Welcome` 메서드를 클릭 한 다음 **뷰 추가**합니다.

여기서는 사용자 **뷰 추가** 같은 대화 상자가 나타납니다.

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

아래에 다음 코드를 추가 합니다 `<h2>` 새 요소 <em>오신 것을 환영 합니다.</em> vbhtml 파일입니다. 루프를 확인 하 고 예를 들어 드리겠습니다 &quot;Hello&quot; 만큼 많은 사용자가 해야 했습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

응용 프로그램을 실행 하 고 이동 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

이제 데이터 URL에서 가져온 것 이며 자동으로 컨트롤러에 전달 됩니다. 컨트롤러에 데이터 패키지는 `Model` 개체와 뷰에 해당 개체를 전달 합니다. 사용자에 게 HTML로 데이터를 표시 하는 보다 뷰.

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

저장소를 일종의 &quot;M&quot; 모델 이지만 데이터베이스 유형은 하지에 대 한 합니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
