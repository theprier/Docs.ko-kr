---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3 부: 보기 및 ViewModels | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 3 부에서는 보기 및 ViewModels를 설명합니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 828ff18abcc5932f82be71a45ebde589eeb051fa
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827537"
---
<a name="part-3-views-and-viewmodels"></a>3 부: 보기 및 ViewModels
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 3 부에서는 보기 및 ViewModels를 설명합니다.


지금까지에서는 했습니다만 된 문자열을 반환 컨트롤러 작업에서. 컨트롤러의 작동 방식을 파악 하는 유용한 방법 이지만 하지는 원하는 실제 웹 응용 프로그램을 빌드하는 것입니다. HTML 사이트를 방문 하는 브라우저를 다시 생성 하는 더 나은 방법을 사용할 예정 – 템플릿 파일 HTML 콘텐츠를 보다 쉽게 사용자 지정에 사용 하는 우리를 반송 합니다. 이것이 뷰 수행 합니다.

## <a name="adding-a-view-template"></a>보기 템플릿 추가

템플릿 보기를 사용 하려면 ActionResult를 반환 하도록 HomeController 인덱스 메서드를 변경 하 고 아래와 같은 View()를 반환 하도록 하겠습니다 했습니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

위의 변경을 나타냅니다.이 반환 되는 대신 문자열 대신 "View"를 사용 하 여 결과 다시 생성 하려고 합니다.

이제 프로젝트에 적절 한 보기 템플릿을 추가 합니다. 이렇게 하려면에서는 인덱스 작업 메서드 내에 텍스트 커서를 배치 다음 마우스 오른쪽 단추로 클릭 고 "추가 보기"를 선택 합니다. 뷰 추가 대화 상자가 표시 됩니다.

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"뷰 추가" 대화 상자를 사용 하면 빠르고 쉽게 보기 템플릿 파일을 생성할 수 있습니다. "추가 보기" 기본적으로 대화 상자를 사용 하는 작업 메서드를 일치 시킬 수 있도록 만드는 보기 템플릿의 이름을 미리 채웁니다. 우리의 HomeController의 index () 작업 메서드 내에서 "추가 보기" 상황에 맞는 메뉴를 사용 하기 때문에 위의 "뷰 추가" 대화 상자에 "Index" 기본적으로 미리 채워진 뷰 이름으로 에서는이 대화 상자에서 옵션 중 하나를 변경 하려면 추가 단추 클릭 필요 없습니다.

추가 단추를 클릭 하면 Visual Web Developer는 존재 하지 않는 경우 폴더를 만들면 \Views\Home 디렉터리에 우리 회사에 뷰 템플릿에 새 Index.cshtml 만들어집니다.

![](mvc-music-store-part-3/_static/image2.png)

"Index.cshtml" 파일의 이름 및 폴더 위치는 중요 하 고 기본 ASP.NET MVC 명명 규칙을 따릅니다. 디렉터리 이름, \Views\Home, HomeController 라는 컨트롤러-일치 합니다. 보기 템플릿 이름으로 인덱스 보기를 표시 하는 컨트롤러 동작 메서드를 찾습니다.

ASP.NET MVC를 사용 하면 뷰를 반환 하려면이 명명 규칙을 사용할 때 이름 또는 뷰 템플릿의 위치를 명시적으로 지정할 필요가 없도록 수 있습니다. 기본적으로 렌더링 됩니다 \Views\Home\Index.cshtml 보기 템플릿에서 HomeController 내에서 아래와 같은 코드를 작성할 때:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

Visual Web Developer가 만들어지고 "뷰 추가" 대화 상자 내에서 "추가" 단추를 클릭 한 후 "Index.cshtml" 보기 템플릿이 열립니다. Index.cshtml의 콘텐츠는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

이 보기에는 ASP.NET Web Forms 및 ASP.NET MVC의 이전 버전에 사용 되는 Web Forms 뷰 엔진 보다 더 간결한는 Razor 구문을 사용 합니다. Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 많은 개발자 들이 Razor 보기 엔진 ASP.NET MVC 개발 잘 맞는.

처음 세 줄 ViewBag.Title를 사용 하 여 페이지 제목을 설정 합니다. 에서는에서는 작동 방식을 자세히 먼저 곧 보겠습니다 업데이트 텍스트 제목 텍스트를 살펴보고 페이지 보기. 업데이트를 &lt;h2&gt; 아래와 같이 "이 되는 홈 페이지"를 태그 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

새 텍스트 홈 페이지에 표시 되는 응용 프로그램은 실행 합니다.

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>일반적인 사이트 요소에 대 한 레이아웃을 사용 하 여

대부분의 웹 사이트에 여러 페이지 간에 공유 되는 내용이: 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등입니다. Razor 보기 엔진 쉽게이 라는 페이지를 사용 하 여 관리할 \_Layout.cshtml에 자동으로 만들어진/뷰/공유 폴더입니다.

![](mvc-music-store-part-3/_static/image4.png)

이 폴더 아래에 나와 있는 내용을 보려면 두 번 클릭 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

개별 뷰에서 콘텐츠를 표시 합니다 @RenderBody() 명령 및 벗어나는 표시 하고자 하는 일반적인 내용을 추가할 수 있습니다는 \_Layout.cshtml 태그입니다. 바로 위의 템플릿에 추가 해 보겠습니다 사이트에서 모든 페이지에는 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더 할 우리의 MVC Music Store 하 려 @RenderBody() 문입니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>스타일 시트를 업데이트 하는 중

빈 프로젝트 템플릿 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다. 일부 추가 CSS 및 이미지 이제에 추가 해 보겠습니다이 사이트의 모양과 느낌을 정의 하는 디자이너 제공 했습니다.

업데이트 된 CSS 파일 및 이미지에서 사용할 수 있는 MvcMusicStore Assets.zip의 콘텐츠 디렉터리에 포함 된 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다. Windows 탐색기에서 둘 다 선택 하 고 아래와 같이 Visual Web developer에서 솔루션의 콘텐츠 폴더에 놓습니다.

![](mvc-music-store-part-3/_static/image5.png)

기존 Site.css 파일을 덮어쓸 것인지 확인 하 라는 메시지가 표시 됩니다. 예를 클릭 합니다.

![](mvc-music-store-part-3/_static/image6.png)

응용 프로그램의 콘텐츠 폴더에 다음과 같이 표시 됩니다.

![](mvc-music-store-part-3/_static/image7.png)

이제 응용 프로그램을 실행 하 고 홈 페이지에서 변경 내용이 어떻게 표시 되는지 확인 하겠습니다.

![](mvc-music-store-part-3/_static/image8.png)

- 변경 된 기능을 검토해 보겠습니다: The HomeController의 Index 작업 메서드에 찾아서 코드 보기 템플릿은 표준 명명 규칙을 따른 때문에 "반환 View()"를 호출 하는 경우에 \Views\Home\Index.cshtmlView 템플릿을 표시 합니다.
- 홈 페이지 \Views\Home\Index.cshtml 보기 템플릿 내에 정의 된 간단한 환영 메시지를 표시 합니다.
- 홈 페이지를 사용 하 여이 \_Layout.cshtml 템플릿 이므로 환영 메시지는 표준 사이트 HTML 레이아웃 내에 포함 됩니다.

## <a name="using-a-model-to-pass-information-to-our-view"></a>정보 보기를 전달 하는 모델을 사용 하 여

방금 하드 코드 된 HTML을 표시 하는 뷰 템플릿이 되지 매우 흥미로운 웹 사이트를 확인 하려고 합니다. 동적 웹 사이트를 만들려면에서는 대신 하려고 우리의 보기 템플릿에 컨트롤러 작업에서 정보를 전달 합니다.

모델-뷰-컨트롤러 패턴 모델 이란 용어는 응용 프로그램에서 데이터를 나타내는 개체입니다. 대개 데이터베이스의 테이블에 모델 개체에 해당 하지만 필요가 없습니다.

ActionResult를 반환 하는 컨트롤러 작업 메서드에서 보기로 모델 개체를 전달할 수 있습니다. 이렇게 하면 적절 한 HTML 응답을 생성 하는 데는 컨트롤러를 응답을 생성 한 다음 보기 템플릿에이 정보를 전달 하는 데 필요한 모든 정보를 명확 하 게 패키지를 수 있습니다. 작업에서 확인 하 여 이해 하 고 시작 하겠습니다 쉽습니다.

먼저 스토어 내 앨범 및 장르를 표현 하는 일부 모델 클래스를 만들어 보겠습니다. 장르 클래스를 만들어 시작 해 보겠습니다. 프로젝트 내에서 "Models" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택 "Genre.cs" 파일의 이름을 합니다.

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

생성 된 클래스에는 공용 문자열 이름 속성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*참고: 궁금한 경우에는 {get; 설정;} 표기법은 수행 하는 C#의 자동 구현 속성 기능을 사용 합니다. 지원 필드를 선언 하기를 요구 하지 않고 속성의 이점을 제공 합니다.*

다음으로 제목과 장르 속성이 있는 앨범 클래스 (Album.cs 라는)를 만들려면 동일한 단계를 따릅니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

이제 모델에서 동적 정보를 표시 하는 뷰를 사용 하 여 StoreController 수정할 수 있습니다. 지금-데모용 우리의 앨범 요청 ID를 기준으로 이름이 것 인 경우-아래 보기와 같이 해당 정보를 표시할 수 했습니다.

![](mvc-music-store-part-3/_static/image10.png)

단일 앨범에 대 한 정보를 표시 하므로 저장소 세부 정보 동작을 변경 하 여 시작 하겠습니다. 맨 위에 "using" 문을 추가 합니다 **StoreControllers** 되므로 앨범 클래스를 사용 하려고 할 때마다 MvcMusicStore.Models.Album를 입력할 필요가 없습니다 MvcMusicStore.Models 네임 스페이스를 포함 하도록 클래스입니다. 해당 클래스의 "using" 섹션을 표시 다음과 같이 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

다음으로, 업데이트 세부 정보 컨트롤러 작업 문자열 보다는 ActionResult 반환 되도록 HomeController의 인덱스 메서드를 사용 하 여 했던 것 처럼.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

이제 보기로 앨범 개체를 반환 하는 논리를 수정할 수 있습니다. 이 자습서의 뒷부분에서 우리는 검색 데이터 데이터베이스에서 하지만 지금은 사용 "더미 데이터"를 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*참고: C#을 사용 하 여 잘 모르는 경우으로 추정할 수 있습니다는 앨범 변수는 런타임에 바인딩된은 var을 사용 하 여 의미 합니다. C# 컴파일러를 사용 하 여 형식 유추 기반으로 새로운는 앨범 형식의 해당 앨범을 인지 합니다. 변수를 할당 하 고 컴파일 시간 검사 및 Visual Studio 코드 편집기를 얻게 되므로 로컬 앨범 변수의 앨범 유형으로 컴파일하는 –는 올바르지 않습니다. 이 옵션을 지원 합니다.*

이제 HTML 응답을 생성 하는 데는 앨범을 사용 하는 템플릿 보기를 만들어 보겠습니다. 작업을 수행 하기 전에 프로젝트를 빌드하려면 뷰 추가 대화 상자에서 새로 만든된 앨범 클래스에 대 한 알 수 있도록 해야 합니다. 메뉴 항목 Debug⇨Build MvcMusicStore를 선택 하 여 프로젝트를 빌드할 수 있습니다 (추가 크레딧을 사용할 수 있습니다 Ctrl-Shift-B 바로 가기 프로젝트를 빌드하려면).

![](mvc-music-store-part-3/_static/image11.png)

지원 클래스를 설정 했으므로 이제 준비가 보기 템플릿은 빌드입니다. 세부 정보 메서드 내에서 마우스 상황에 맞는 메뉴에서 "추가 보기..."를 선택 합니다.

![](mvc-music-store-part-3/_static/image12.png)

HomeController를 사용 하 여 전에 수행한 것과 같이 새 보기 템플릿을 만들려면 예정입니다. StoreController에서 만드는 것 때문에 기본적으로 생성 됩니다 \Views\Store\Index.cshtml 파일에 있습니다.

달리 이전 하겠습니다 "강력한 형식의 만들기" 보기 확인란 합니다. 그런 다음 하겠습니다 "보기 데이터-클래스" drop downlist 내 "앨범" 클래스를 선택 합니다. 이렇게 하면 개체를 사용 하 여 전달할 앨범을 필요로 하는 뷰 템플릿을 만들려면 "뷰 추가" 대화 상자.

![](mvc-music-store-part-3/_static/image13.png)

"추가" 단추를 클릭할 때 \Views\Store\Details.cshtml 보기 템플릿은 만들어집니다, 다음 코드를 포함 하 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

이 보기는 강력한 앨범 클래스를 나타내는 첫 번째 줄을 확인 합니다. Razor 보기 엔진 이해 되었습니다 통과 했다고 앨범 개체를 쉽게 모델 속성에 액세스 하는 Visual Web Developer 편집기의 IntelliSense의 이점은 있을 수 있도록 합니다.

업데이트를 &lt;h2&gt; 태그는 Album Title 속성이 다음과 같이 표시할 줄을 수정 하 여 표시 하도록 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

뒤에 마침표를 입력 하면 IntelliSense 트리거한 확인는 @Model 키워드, 앨범 클래스를 지 원하는 메서드와 속성을 표시 합니다.

보겠습니다 이제 프로젝트를 다시 실행 하 고 저장소/세부 정보/5 URL을 방문 하세요. 아래와 같은 앨범의 세부 정보를 살펴보겠습니다.

![](mvc-music-store-part-3/_static/image14.png)

이제 저장소 찾아보기 동작 메서드에 대 한 유사한 업데이트를 만들 수 것입니다. ActionResult를 반환 하도록 메서드를 업데이트 하 고 새 장르 개체를 만들고 뷰를 반환 하므로 메서드는 논리를 수정 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

뷰를 강력한 형식의 추가한 찾아보기 메서드를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 "추가 보기..."를 선택 강력한 형식의 장르 클래스에 추가 합니다.

![](mvc-music-store-part-3/_static/image15.png)

업데이트를 &lt;h2&gt; 뷰에서 요소 코드 (/Views/Store/Browse.cshtml) 장르 정보를 표시 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

이제 프로젝트를 다시 실행 하 고/저장소/찾아보기로 이동 하겠습니다. 장르 = Disco URL입니다. 아래와 비슷하게 표시 되지만 찾아보기 페이지를 살펴보겠습니다.

![](mvc-music-store-part-3/_static/image16.png)

마지막으로 약간 더 복잡 한 업데이트를 확인 합니다 **인덱스 저장** 작업 메서드 및 스토어에서 모든 장르 목록을 표시 하려면 보기. 장르 목록 장르를 방금 아닌은 모델 개체를 사용 하 여 수행 됩니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

저장소 인덱스 작업 메서드에서 마우스 추가 뷰 이전 모델 클래스로 장르를 선택 하 고 추가 단추를 눌러 선택 합니다.

![](mvc-music-store-part-3/_static/image17.png)

에서는 변경 먼저는 @model 하나만 대신 선언 뷰는 몇 가지 장르 예상 수를 나타내는 개체입니다. 첫 번째 부분은 /Store/Index.cshtml을 다음과 같이 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

몇 가지 장르 개체를 보유할 수 있는 모델 개체를 사용 하 여 작동 하는 Razor 보기 엔진을 인지를 나타냅니다. IEnumerable을 사용 하는 것&lt;장르&gt; 목록 대신&lt;장르&gt; 보다 일반적인 이므로 IEnumerable 인터페이스를 지 원하는 모든 개체 형식에는 모델 형식을 나중에 변경할 수 있도록 합니다.

그런 다음 아래 코드는 완료 된 보기에 표시 된 대로 모델의 장르 개체 반복 됩니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

있습니다 전체 IntelliSense 지원이이 코드를 입력으로 입력 하면 되도록 "@Model." 모든 메서드 및 장르 형식의 IEnumerable을 지 원하는 속성을 참조 했습니다.

![](mvc-music-store-part-3/_static/image18.png)

"foreach" 루프 내에서 Visual Web Developer는 각 항목 이므로 Genre 형식의 각각에 대해 IntelliSense를 볼 장르 형식 알고 있습니다.

![](mvc-music-store-part-3/_static/image19.png)

다음으로, 스 캐 폴딩 기능은 장르 개체를 검사 및 각 되어 Name 속성을 반복 하 고 작성 하 있도록 결정 합니다. 또한 각 개별 항목에 대 한 편집, 세부 정보 및 삭제 링크를 생성합니다. 에서는 사용 하는 나중에 저장소 관리자에에서 있지만 지금은 목록이 간단한 대신 하고자 합니다.

응용 프로그램을 실행 하 고 /Store 이동, 개수 및 장르 목록을 모두 표시 되도록을 참조 합니다.

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>페이지 간 링크를 추가합니다.

/Store URL 현재 장르를 나열 하는 일반 텍스트로 단순히 장르 이름을 나열 합니다. 바꿔보겠습니다 일반 텍스트 대신 대신 수 있도록 적절 한 저장소/찾아보기 URL 장르 이름 링크를 "Disco" 이동/저장소/찾아보기와 같은 음악 장르를 클릭할 수 있도록? 장르 = Disco URL입니다. 다음이 링크를 사용 하 여 아래와 같은 코드 출력 \Views\Store\Index.cshtml 보기 템플릿은 업데이트 수 **(이 입력 하지 않은-를 개선 하려고)**:

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

이런 방법도 있지만 하드 코드 된 문자열에 의존 하므로 나중에 문제를 발생할 수 있습니다. 예를 들어 컨트롤러를 바꾸려면 싶으면 업데이트 해야 하는 링크에 대 한 확인 코드를 통해 검색 해야 합니다.

대 안으로 사용할 수 있습니다는 HTML 도우미 메서드를 활용 하는 것입니다. ASP.NET MVC는 다양 한이 같은 일반적인 작업을 수행 하는 보기 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드를 포함 합니다. Html.ActionLink() 도우미 메서드는 특히 유용 합니다 및 HTML 빌드 쉽게 &lt;는&gt; 링크 및 URL 경로 URL로 인코딩된 제대로 되었는지 같은 성가신 세부 사항을 처리 합니다.

Html.ActionLink() 링크에 필요한 만큼 많은 정보를 지정할 수 있도록 몇 가지 다른 오버 로드에 있습니다. 가장 간단한 경우에만 링크 텍스트 및 클라이언트에서 하이퍼링크를 클릭할 때 이동할 작업 메서드를 입력 합니다. 예를 들어, "저장소 /" "이동 하는 저장소 인덱스" 다음 호출을 사용 하 여 링크 텍스트를 사용 하 여 저장소 세부 정보 페이지의 index () 메서드를 연결할 수 했습니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*참고:이 예에서는 필요가 없었습니다 현재 보기를 렌더링 하는 동일한 컨트롤러 내의 다른 작업에만 연결 하는 것 때문에 컨트롤러의 이름을 지정 합니다.*

찾아보기 페이지에 대 한 링크는 3 개의 매개 변수는 Html.ActionLink 메서드의 다른 오버 로드 사용 하므로 매개 변수 전달, 그러나 해야 합니다.

- 1. 장르 이름을 표시 하는 링크 텍스트
- 2. 컨트롤러 작업 이름 (찾아보기)
- 3. 경로 매개 변수 값을 이름 (장르)과 값 (장르 이름)를 지정 합니다.

모두를 함께 여기서는 저장소 인덱스 보기에 이러한 링크를 작성 하는 방법을 배치 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

이제 프로젝트를 다시 실행 하 고 /Store/ URL에 액세스 하는 경우 장르 목록이 표시 됩니다 것입니다. 클릭할 때 하이퍼링크 – 각 장르에는 우리의/저장소 / 찾아보기 걸립니다? 장르 =*[장르]* URL입니다.

![](mvc-music-store-part-3/_static/image3.jpg)

장르 목록에 대 한 HTML은 다음과 같습니다.

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-2.md)
> [다음](mvc-music-store-part-4.md)
