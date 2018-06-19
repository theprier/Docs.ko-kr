---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3 부: 뷰와 Viewmodel | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 3 부에서는 뷰 및 Viewmodel 다룹니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 497c2898db2e03b0650982c3ad1e6b5ac5ca639d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874852"
---
<a name="part-3-views-and-viewmodels"></a>3 부: 뷰와 Viewmodel
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 3 부에서는 뷰 및 Viewmodel 다룹니다.


지금까지 म 했습니다 방금 된 문자열에서에서 반환 컨트롤러 작업. 컨트롤러의 작동 방식을 파악 하는 좋은 방법이 하지만 하지 어떻게 원할 실제 웹 응용 프로그램을 빌드하는 것이 쉽습니다. 사이트를 방문 하는 브라우저에 다시 HTML을 생성 하기 위해 더 좋은 방법은 원하는 하겠습니다-템플릿 파일 보다 쉽게 HTML 콘텐츠를 사용자 지정 하려면 사용할 수는 있는 하나를 다시 보낼 합니다. 뷰가 수행할 정확 하 게입니다.

## <a name="adding-a-view-template"></a>보기 템플릿 추가

템플릿 보기를 사용 하려면 있는 ActionResult를 반환할 HomeController 인덱스 방법 변경 알아보고 아래와 같은 View()를 반환 하도록 하겠습니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

대신 "보기"를 사용 하 여 결과 다시 생성 하려고, 위의 변경 내용을 문자열로 반환 대신 되었음을 나타냅니다.

이제이 프로젝트에는 적절 한 보기 템플릿을 추가 합니다. 이렇게 하려면 인덱스 작업 메서드 내에서 텍스트 커서의 위치를 한 다음 마우스 오른쪽 단추로 클릭 알아보고 하겠습니다 "추가 보기"를 선택. 그러면 뷰 추가 대화 상자를 표시 됩니다.

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"뷰 추가" 대화 상자를 쉽고 빠르게 보기 템플릿 파일을 생성할 수 있습니다. "추가 된 보기" 기본적으로 대화 상자를 사용 하 여 동작 메서드가 일치 하도록 만드는 보기 템플릿의 이름을 미리 채웁니다. 우리의 HomeController의 index () 동작 메서드 내에서 "추가 보기" 상황에 맞는 메뉴를 사용 하기 때문에 위의 "뷰 추가" 대화 자기 "Index" 기본적으로 미리 채워진 뷰 이름입니다. 이 대화 상자에서 옵션 변경, 이므로 추가 단추를 클릭 합니다. 필요 하지 않습니다.

추가 단추를 클릭 하면 Visual Web Developer 보기 서식 파일을 수행해 줍니다 경우 폴더를 만들면 \Views\Home 디렉터리에 존재 하지 않는 새 Index.cshtml 만들어집니다.

![](mvc-music-store-part-3/_static/image2.png)

"Index.cshtml" 파일의 이름과 폴더 위치는 중요 하며, 기본 ASP.NET MVC 명명 규칙을 따릅니다. 디렉터리 이름, \Views\Home, HomeController 이름으로 지정 된 컨트롤러와 일치 합니다. 보기 템플릿 이름, 인덱스, 보기를 표시 하는 컨트롤러 동작 메서드를 찾습니다.

ASP.NET MVC는 뷰를 반환 하려면이 명명 규칙을 사용 하면 이름 또는 뷰 서식 파일의 위치를 명시적으로 지정할 필요가 없도록를 수 있습니다. 기본적으로 렌더링 합니다 \Views\Home\Index.cshtml 보기 템플릿 우리의 HomeController 내에서 아래와 같은 코드를 작성 했습니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

Visual Web Developer 만들어지고 템플릿 "Index.cshtml" 보기 "뷰 추가" 대화 상자 내에서 "추가" 단추를 클릭 했습니다. Index.cshtml의 내용은 아래에 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

이 보기는 ASP.NET Web Forms 및 이전 버전의 ASP.NET MVC에서 사용 하는 Web Forms 뷰 엔진이 보다 더욱 간결 하 게 하는 Razor 구문을 사용 중입니다. Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 많은 개발자 들이 Razor 뷰 엔진 ASP.NET MVC 개발 잘 맞는 합니다.

처음 세 줄 ViewBag.Title를 사용 하 여 페이지 제목을 설정 합니다. 페이지 보기 알아보고 텍스트 제목 텍스트가 과정에서 자세히 곧 하지만 먼저 보겠습니다 업데이트를 확인 하겠습니다. 업데이트는 &lt;h2&gt; 아래와 같이 "이 되는 홈 페이지"를 태그 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

응용 프로그램은 홈 페이지에 표시 되는 새 텍스트를 실행 합니다.

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>일반적인 사이트 요소에 대 한 레이아웃을 사용 하 여

대부분의 웹 사이트에는 여러 페이지 간에 공유 되는 콘텐츠가 있는: 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등입니다. Razor 뷰 엔진을 편리 라는 페이지를 사용 하 여 관리할 \_Layout.cshtml 자동으로 작성 된 우리/뷰/공유 폴더에 있습니다.

![](mvc-music-store-part-3/_static/image4.png)

아래에 표시 됩니다는 내용을 보려면이 폴더에 두 번 클릭 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

우리의 개별 보기에서 콘텐츠를 표시 하는 @RenderBody() 명령 및 있는 외부에서 표시 하려는 기타 일반적인 콘텐츠 배포에 추가할 수는 \_Layout.cshtml 태그입니다. MVC 음악 스토어 있도록 바로 위에 있는 서식 파일에 추가 하는 사이트에 있는 모든 페이지는 홈 페이지 및 저장소 영역에 대 한 링크가 있는 공용 헤더를 할 수 있음 @RenderBody() 문입니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>스타일 시트를 업데이트합니다.

빈 프로젝트 템플릿 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일에 포함 됩니다. 디자이너 우리의 몇 가지 추가 CSS 이미지를 제공 지금에 추가 하므로 사이트에 대 한 디자인을 정의 합니다.

업데이트 된 CSS 파일 및 이미지에서 제공 되는 MvcMusicStore Assets.zip의 콘텐츠 디렉터리에 포함 된 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다. Windows 탐색기에서 둘 모두를 선택 하 고 아래와 같이 Visual Web Developer에서 솔루션의 콘텐츠 폴더를 삭제 합니다.

![](mvc-music-store-part-3/_static/image5.png)

기존 Site.css 파일을 덮어쓸 것인지를 확인 하 라는 메시지가 표시 됩니다. 예를 클릭 합니다.

![](mvc-music-store-part-3/_static/image6.png)

응용 프로그램의 콘텐츠 폴더에 다음과 같이 표시 됩니다.

![](mvc-music-store-part-3/_static/image7.png)

이제 응용 프로그램을 실행 하 고 홈 페이지에서 변경 내용이 어떻게 표시 되는지 확인 하겠습니다.

![](mvc-music-store-part-3/_static/image8.png)

- 변경 된 기능을 검토해 보겠습니다: 및의 HomeController 인덱스 동작 메서드가 두 개 우리의 보기 템플릿 뒤에 표준 명명 규칙 때문에 코드에 "반환 View()" 라고 하는 경우에 \Views\Home\Index.cshtmlView 서식 파일을 표시 합니다.
- 홈 페이지를 \Views\Home\Index.cshtml 보기 템플릿 내에 정의 된 간단한 환영 메시지를 표시 합니다.
- 홈 페이지를 사용 하 여 우리의 \_Layout.cshtml 템플릿을 시작 메시지 표준 사이트 HTML 레이아웃 내에 포함 되어 있으므로 합니다.

## <a name="using-a-model-to-pass-information-to-our-view"></a>모델을 사용 하 여이 보기에 정보를 전달

방금 하드 코드 된 HTML을 표시 하는 뷰 템플릿이 없는 매우 흥미로운 웹 사이트를 확인 하려고 합니다. 동적 웹 사이트를 만들려면 것 대신 하고자 우리의 템플릿 보기에는 컨트롤러 작업에서 정보를 전달 합니다.

모델-뷰-컨트롤러 패턴 모델 이란 용어는 응용 프로그램에서 데이터를 나타내는 개체입니다. 모델 개체에 해당 데이터베이스의 테이블은 대개 하지만 필요가 없습니다.

컨트롤러 작업 메서드에 있는 ActionResult를 반환 하는 보기에 모델 개체를 전달할 수 있습니다. 따라서 적절 한 HTML 응답을 생성 하는 데 응답을 생성 하 고 다음 템플릿 보기를이 정보를 전달 하는 데 필요한 모든 정보를 명확 하 게 패키지에는 컨트롤러 수 있습니다. 이제 시작 하겠습니다 하므로, 작업에서 확인 하 여 이해 하기 가장 쉽고입니다.

먼저 스토어 내의 장르와 앨범을 나타내기 위해 일부 모델 클래스를 만들어 보겠습니다. 장르 클래스를 만들어 보겠습니다. 프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택한 파일의 이름을 "Genre.cs"입니다.

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

생성 된 클래스에 공용 string Name 속성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*참고: 본다면, 경우에는 {get; 설정;을 (를) 표기 하는 C#의 자동 구현 속성 기능을 사용 합니다. 이 목록에 속성의 이점을 없이 지원 필드를 선언할 수 있습니다.*

다음으로 제목 및 장르 속성이 있는 앨범 클래스 (Album.cs 라고 함)를 만들려면 동일한 단계를 따릅니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

이제이 모델에서 동적 정보를 표시 하는 뷰를 사용 하도록 StoreController 수정할 수 있을 합니다. 경우-설명을 위해 지금은-이름을 요청 ID에 따라 우리의 앨범, 아래의 보기에서와 같이 해당 정보를 표시할 수 있습니다.

![](mvc-music-store-part-3/_static/image10.png)

단일 앨범에 대 한 정보를 표시 하므로 저장소 세부 정보 동작을 변경 하 여 시작 합니다. 맨 위에 "using" 문을 추가 **StoreControllers** 클래스 앨범 클래스를 사용 하 려 할 때마다 MvcMusicStore.Models.Album 입력할 필요가 없습니다 MvcMusicStore.Models 네임 스페이스를 포함 합니다. 해당 클래스의 "using" 섹션 표시 되 고 다음과 같이 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

다음으로 업데이트 하는 세부 정보 컨트롤러 동작은 문자열이 아니라는 ActionResult 반환 되도록 HomeController의 Index 메서드와 동일한 방식으로.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

이제 보기로 앨범 개체를 반환 하는 논리를 수정할 수 있습니다. 이 자습서의 뒷부분에 나오는 우리는 수 데이터는 데이터베이스에서 검색 – 하지만 지금 바로 사용 합니다 "데이터는 dummy"를 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*참고: C#과 함께 잘 모르는 경우으로 추정할 수 있습니다이 앨범 변수는 런타임에 바인딩 이라는 var을 사용 하 여 의미 합니다. C# 컴파일러에서 형식 유추를 기반으로 하는 해당 앨범이 유형이 앨범을 결정 하는 변수에 할당 및 기능 컴파일 타임 검사 및 Visual Studio code 편집기 하므로 로컬 앨범 변수 앨범 유형으로 컴파일할를 사용 하는 –는 올바르지 않습니다. 이 옵션을 지원 합니다.*

이제 우리의 앨범을 사용 하 여 HTML 응답을 생성 하는 보기 서식 파일을 만들어 보겠습니다. 그 전에 프로젝트를 빌드하려면 뷰 추가 대화 상자는 새로 만든된 앨범 클래스에 대 한 알 수 있도록 해야 합니다. 메뉴 항목 Debug⇨Build MvcMusicStore를 선택 하 여 프로젝트를 빌드할 수 있습니다 (추가 신용에 대 한 사용할 수 있습니다 Ctrl-Shift-B 바로 가기 프로젝트를 빌드하려면).

![](mvc-music-store-part-3/_static/image11.png)

지원 클래스를 설정 했으므로 준비가 우리의 보기 서식 파일을 작성 합니다. 세부 정보 메서드 내에서 마우스 오른쪽 단추로 누르고 "추가 보기..." 상황에 맞는 메뉴입니다.

![](mvc-music-store-part-3/_static/image12.png)

HomeController 사용 하기 전에 수행한 것 처럼 새 보기 템플릿을 만들려면 하겠습니다. StoreController에서 만드는 것 때문에 기본적으로 생성 됩니다 \Views\Store\Index.cshtml 파일에 있습니다.

와 달리 이전에 것 이며 "강력한 형식의 만들기" 보기 확인란을 선택 합니다. 다음을 하겠습니다 "데이터-클래스 보기" 드롭 downlist 내에서 "앨범" 클래스를 선택 합니다. 이렇게 하면 개체를 사용 하도록에 전달 될 앨범에는 필요한 뷰 템플릿을 만들려면 "뷰 추가" 대화 상자.

![](mvc-music-store-part-3/_static/image13.png)

"추가" 단추를 클릭 하면 다음 코드가 포함 된, 우리의 \Views\Store\Details.cshtml 보기 템플릿을 만들 수 됩니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

첫 번째 줄이이 보기에서는 앨범 클래스에 강력한 형식의 하다는 것을 확인 합니다. Razor 뷰 엔진 되었습니다 통과 했다고 앨범 개체 하므로 쉽게 모델 속성에 액세스 하 고 Visual Web Developer 편집기에서 IntelliSense는 이점이 있을 수를 이해 합니다.

업데이트는 &lt;h2&gt; 태그를 다음과 같이 표시 해당 줄을 수정 하 여 앨범의 Title 속성을 표시 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

뒤에 마침표를 입력 하는 때 IntelliSense 트리거되는 것을 알는 @Model 키워드, 속성 및 앨범 클래스에서 지 원하는 메서드를 표시 합니다.

보겠습니다 이제이 프로젝트를 다시 실행 하 고 저장소/세부 정보/5 URL을 방문 합니다. 아래와 같은 앨범의 세부 정보를 살펴보겠습니다.

![](mvc-music-store-part-3/_static/image14.png)

이제 저장소 찾아보기 동작 메서드에 대 한 유사한 업데이트를 만들면 됩니다. ActionResult 반환 하도록 메서드를 업데이트 하 고 메서드 논리를 수정 하 여 새 장르 개체를 만들고 있으므로 보기로 돌아갑니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

찾아보기 메서드 단추로 클릭 하 고 "추가 보기..."를 선택 합니다. 상황에 맞는 메뉴에서 다음 보기를 강력한 형식의 추가 강력한 형식의 장르 클래스에 추가 합니다.

![](mvc-music-store-part-3/_static/image15.png)

업데이트는 &lt;h2&gt; 보기의 요소 (의 코드 /Views/Store/Browse.cshtml) 장르 정보를 표시 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

이제이 프로젝트를 다시 실행 하 고 찾아보기/저장소/찾아보기 하겠습니다. 장르 디스코 URL = 합니다. 찾아보기 페이지와 같은 아래에 표시를 살펴보겠습니다.

![](mvc-music-store-part-3/_static/image16.png)

마지막으로, आ म च ी에 대 한 약간 더 복잡 한 업데이트는 **저장 인덱스** 작업 메서드와 뷰를 스토어에 모든 장르의 목록을 표시 합니다. 단일 장르 뿐이 아닌 모델 개체는 장르 목록을 사용 하 여를 하겠습니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

저장소 인덱스 작업 메서드에서 고 이전에 모델 클래스로 장르를 선택 하 고 추가 단추를 눌러 처럼 뷰 추가 선택 합니다.

![](mvc-music-store-part-3/_static/image17.png)

먼저 변경 합니다는 @model 하나만 대신 나타내려면 보기 여러 장르 제공 될 개체입니다. 다음과 같이 /Store/Index.cshtml의 첫 번째 줄을 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

작업 하는 여러 장르 개체를 저장할 수 있는 모델 개체와 함께 Razor 뷰 엔진을 인지를 나타냅니다. IEnumerable에서는&lt;장르&gt; 목록 대신&lt;장르&gt; 일반적 이므로, IEnumerable 인터페이스를 지 원하는 모든 개체 형식에 나중에 모델 유형을 변경 하도록 허용 합니다.

그런 다음 아래 코드 완성 된 보기에에서 표시 된 대로 모델의 장르 개체 반복 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

있는지 완벽 하 게 IntelliSense 지원에서는이 코드를 입력 하는 대로 입력할 때 있도록 공지 "@Model." 메서드 및 형식 Genre의 IEnumerable에서 지 원하는 속성 모두 표시 합니다.

![](mvc-music-store-part-3/_static/image18.png)

우리의 "foreach" 루프 내 Visual Web Developer 임을 알고 각 항목 장르 형식의 IntelliSence 각각에 대해 표시 되므로 장르 형식이 있습니다.

![](mvc-music-store-part-3/_static/image19.png)

다음으로, 스 캐 폴딩 기능 장르 개체를 검사 하 고 확인 하므로 전체를 반복 하 고 작성 하는 Name 속성이 했습니다 됩니다 각각. 또한 각 개별 항목에 대 한 편집, 정보 및 삭제 링크를 생성합니다. 활용 하는 저장소 관리자 인의 뒷부분에 나오는 살펴보겠습니다 하지만 지금은 간단한 목록 대신가 싶습니다.

응용 프로그램을 실행 하 고 /Store 찾아보기, 개수와 장르 목록에 표시 되도록 표시 됩니다.

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>페이지 간 링크 추가

현재 장르를 나열 하 여 /Store URL 일반 텍스트로 단순히 장르 이름을 나열 합니다. 보겠습니다이 모양을 변경 할 수 있도록 하는 대신 일반 텍스트 대신 적절 한 저장소/찾아보기 URL에 대 한 장르 이름 링크를 클릭 하면 "Disco" / 저장소/찾아보기도 이동 되는 like 음악 장르? 장르 = Disco URL입니다. 이러한 링크를 사용 하 여 아래와 같은 코드 출력으로 우리의 \Views\Store\Index.cshtml 뷰 템플릿을 업데이트할 수 있습니다 **(에 입력 하지 않은-에 개선 하 여)**:

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

에 성공 하지만 하드 코드 된 문자열에 의존 하므로 나중에 문제를 발생할 수 있습니다. 예를 들어, 컨트롤러의 이름을 바꾸려면 있으니까요 해야 우리의 원하는 코드를 업데이트 해야 하는 링크를 통해 검색 합니다.

다른 방법은 사용할 수는 HTML 도우미 메서드를 활용 하는 합니다. ASP.NET MVC는 다양 한이 같은 일반적인 작업을 수행 하는 보기 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드를 포함 합니다. Html.ActionLink() 도우미 메서드는은 특히 유용 한을 손쉽게 HTML 만들려는 &lt;는&gt; 연결 하는 URL로 인코딩된 URL 경로가 제대로 확인 같은 번거로울 세부 사항을 처리 합니다.

Html.ActionLink() 링크에 필요한 만큼 많은 정보를 지정할 수는 몇 가지 다른 오버 로드에 있습니다. 가장 간단한 경우 고 링크 텍스트와 클라이언트에서 하이퍼링크를 클릭할 때 이동할 동작 메서드를 입력 합니다. 예를 들어 "/ 저장소 /" 된 링크 텍스트 이동에 저장소 "인덱스" 다음 호출을 사용 하는 저장소 세부 정보 페이지 index () 메서드를 연결할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*참고:이 경우 하지 않은 해야 것 바로 연결 하 고 현재 뷰를 렌더링 하는 동일한 컨트롤러에서 다른 작업 때문에 컨트롤러의 이름을 지정 합니다.*

찾아보기 페이지에 대 한 링크는 세 가지 매개 변수를 사용 하는 Html.ActionLink 메서드의 다른 오버 로드에서는 하므로 매개 변수 전달, 하지만 필요 합니다.

- 1. 링크 텍스트는 장르 이름이 표시 됩니다
- 2. 컨트롤러 동작 이름 (찾아보기)
- 3. (장르) 이름 및 값 (장르 이름)을 모두 지정 하는 경로 매개 변수 값

배치 한꺼번에 모두 여기 인지 어떻게 이러한 링크 저장소 인덱스 뷰를 작성 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

이제이 프로젝트를 다시 실행 하 고 /Store/ URL에 액세스 했습니다 장르 목록을 표시 됩니다. 클릭할 때 각각은 하이퍼링크 – us에 걸리는 우리의/저장소/찾아보기? 장르 =*[장르]* URL입니다.

![](mvc-music-store-part-3/_static/image3.jpg)

HTML 장르 목록에는 다음과 같습니다.

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-2.md)
> [다음](mvc-music-store-part-4.md)
