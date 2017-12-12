---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: "ASP.NET 웹 페이지를 소개-일관 된 레이아웃 만들기 | Microsoft Docs"
author: tfitzmac
description: "이 자습서에서는 레이아웃을 사용 하 여 페이지에 일관 된 모양을 ASP.NET 웹 페이지를 사용 하는 사이트를 만들려고 하는 방법을 보여 줍니다. 완료 한 것으로 가정는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 692adc5a03892f27c91fe8868c8eab6ce08f49cd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET 웹 페이지-일관 된 레이아웃 만들기 소개
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서를 사용 하는 방법을 보여 줍니다. *레이아웃* 페이지에 일관 된 모양을 ASP.NET 웹 페이지를 사용 하는 사이트를 만들려고 합니다. 통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지에서 데이터베이스 데이터 삭제](https://go.microsoft.com/fwlink/?LinkId=251584)합니다.
> 
> 학습 내용:
> 
> - 레이아웃 페이지가입니다.
> - 동적 콘텐츠가 있는 레이아웃 페이지를 결합 하는 방법입니다.
> - 레이아웃 페이지에 값을 전달 하는 방법.


## <a name="about-layouts"></a>레이아웃 정보

지금까지 만든 페이지 모두 완료 된, 독립 실행형 페이지입니다. 동일한 사이트에 속한 모두 있지만 없습니다 모든 공통 요소 또는 표준 모양입니다.

대부분의 사이트는 일관 된 모양과 레이아웃 필요가 있습니다. 예를 들어, 이동 하는 경우는 [Microsoft.com/web](https://www.microsoft.com/web/) 사이트 및 둘러보세요를 모든 페이지 전체 레이아웃을 시각적 테마를 준수 하는 것이 표시:

![헤더, 탐색 영역, 콘텐츠 영역 및 바닥글의 레이아웃을 보여 주는 Microsoft.com/web 사이트 페이지](layouts/_static/image1.png)

*비효율적인* 이 레이아웃을 만드는 방법은 각 페이지에 머리글, 탐색 모음과 바닥글을 개별적으로 정의 하는 것입니다. 사용자는 복제 동일한 태그 될 때마다 합니다. 옵션을 변경 하려는 경우 (예를 들어 업데이트 바닥글) 각 페이지를 개별적으로 변경 해야 합니다.

Where 즉 *레이아웃 페이지* 와 야 합니다. ASP.NET 웹 페이지에서 사이트에 있는 페이지에 대 한 전체 컨테이너를 제공 하는 레이아웃 페이지를 정의할 수 있습니다. 예를 들어, 레이아웃 페이지, 탐색 영역에서 머리글과 바닥글을 포함할 수 있습니다. 레이아웃 페이지 주 콘텐츠 흐름 방향은 자리 표시자를 포함 합니다.

다음 태그와 해당 페이지에만 대 한 코드를 포함 하는 개별 콘텐츠 페이지를 정의할 수 있습니다. 콘텐츠 페이지를 HTML 페이지 전체; 쓸 필요가 없습니다. 가 전환할 필요도 `<body>` 요소입니다. 레이아웃 페이지의 콘텐츠를 표시 하려면 ASP.NET 지시 하는 코드 줄도 갖게 됩니다. 다음은이 관계의 작동 원리 대략 보여 주는 그림이입니다.

![두 콘텐츠 페이지 및 들어갈 있는 레이아웃 페이지를 보여 주는 개념 다이어그램](layouts/_static/image2.png)

이 상호 작용 작업에서 참조 하는 경우를 이해 하기 쉽습니다. 이 자습서에서는 레이아웃을 사용 하 여 동영상 페이지를 변경 합니다.

## <a name="adding-a-layout-page"></a>레이아웃 페이지 추가

머리글, 바닥글 및 주 콘텐츠에 대 한 영역에 있는 일반적인 페이지 레이아웃을 정의 하는 레이아웃 페이지를 만들어 시작 합니다. WebPagesMovies 사이트에서 추가 라는 CSHTML 페이지  *\_Layout.cshtml*합니다.

선행 밑줄 ( `_` ) 문자는 매우 중요 합니다. 페이지의 이름은 밑줄로 시작 되 면 ASP.NET 브라우저에 해당 페이지를 직접 보내지 않습니다. 이 규칙은 사이트에 필요한 없지만 사용자가 직접 요청할 수 아니어야 합니다. 페이지를 정의할 수 있습니다.

다음 페이지의 내용을 바꿉니다.

[!code-html[Main](layouts/samples/sample1.html)]

이 태그는 HTML을 사용 하는 바로 볼 수 있듯이 `<div>` 더 페이지와 1에서 3 개의 섹션을 정의 하는 요소 `<div>` 세 개의 섹션을 보유 하는 요소입니다. Razor 코드의 비트를 포함 하는 바닥글: `@DateTime.Now.Year`, 페이지의 위치에 있는 현재 연도 렌더링 합니다입니다.

명명 된 스타일 시트에 대 한 링크는 *Movies.css*합니다. 스타일 시트는 요소의 실제 레이아웃의 세부 정보는 정의 하는 위치입니다. 잠시 후에 만들어야 합니다.

이 독특한 기능  *\_Layout.cshtml* 페이지는는 `@Render.Body()` 선입니다. 이 레이아웃은 다른 페이지와 병합 될 때 콘텐츠 어디로 자리 표시자입니다.

## <a name="adding-a-css-file"></a>.Css 파일 추가

해당 페이지에서 요소의 실제 정렬 (즉, 모양)을 정의 하는 기본 방법은 연계 스타일 시트 (CSS) 규칙을 사용 하는 것입니다. 만들 수 있도록 한 *.css* 새 레이아웃에 대 한 규칙을 포함 하는 파일입니다.

WebMatrix에서 사이트의 루트를 선택 합니다. 그런 다음는 **파일** 탭 리본 메뉴의 아래의 화살표를 클릭 합니다.는 **새로** 단추를 선택한 다음 클릭 **새 폴더**합니다.

![리본에서 새로 ' 새 폴더 ' 옵션입니다.](layouts/_static/image3.png)

새 폴더 이름을 *스타일*합니다.

![새 폴더 '스타일' 이름 지정](layouts/_static/image4.png)

새로운 내부 *스타일* 폴더 라는 파일을 만들어 *Movies.css*합니다.

![새 Movies.css 파일 만들기](layouts/_static/image5.png)

새 내용을 바꾸는 *.css* 다음 파일:

[!code-css[Main](layouts/samples/sample2.css)]

두 가지를 확인을 제외 하 고 이러한 CSS 규칙에 대해 잘 다루지 합니다. 하나는 글꼴 및 크기를 설정 하는, 규칙 사용 하 여 절대 위치 설정 머리글, 바닥글 및 주 콘텐츠 영역의 위치입니다. 읽을 수 있으면를 처음 접하는 CSS에 배치 하는 [CSS 위치](http://www.w3schools.com/css/css_positioning.asp) W3Schools 사이트 자습서입니다.

에 개별적으로 정의 아래쪽에서 우리 스타일 규칙 원래을 복사 했는지 확인 하는 것은 *Movies.cshtml* 파일입니다. 이러한 규칙에 사용 된는 [데이터를 표시 하 여 사용 하 여 ASP.NET 웹 페이지 소개](https://go.microsoft.com/fwlink/?LinkId=251580) 확인 하기 위해 자습서는 `WebGrid` 도우미 테이블에 줄무늬를 추가 하는 태그를 렌더링 합니다. (사용 하는 경우는 *.css* 파일 스타일 정의 대 한 수도 기록 하는 전체 사이트에 대 한 스타일 규칙입니다.)

## <a name="updating-the-movies-file-to-use-the-layout"></a>레이아웃을 사용 하 여 영화 파일 업데이트

이제 새 레이아웃을 사용 하도록 사이트를 기존 파일을 업데이트할 수 있습니다. 열기는 *Movies.cshtml* 파일입니다. 맨 위에 있는 코드의 첫 번째 줄으로 다음을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample3.cs)]

페이지는이 방법으로 이제 시작 됩니다.

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

이 한 줄의 코드 asp 때는 *동영상* 페이지가 실행와 병합 해야는  *\_Layout.cshtml* 파일입니다.

이후는 *Movies.cshtml* 레이아웃 페이지에 이제 사용 하 여 파일에서 태그를 제거할 수는 *Movies.cshtml* 에서 처리에 있는 페이지는  *\_Layout.cshtml*파일입니다. 꺼내서는 `<!DOCTYPE>`, `<html>`, 및 `<body>` 태그 및 닫는 태그입니다. 전체 꺼내서 `<head>` 요소와 해당 규칙에 있으므로 이제 이후 눈금에 대 한 스타일 규칙을 포함 하는 해당 콘텐츠는 *.css* 파일입니다. 에 있을 때 기존 변경 `<h1>` 요소는 `<h2>` 요소;는 `<h1>` 이미 레이아웃 페이지의 요소입니다. 변경 된 `<h2>` 텍스트 "동영상 목록"입니다.

일반적으로 콘텐츠 페이지에 변경이 내용을 확인 해야 할가 있습니다. 레이아웃 페이지를 사이트를 시작 하면 이러한 모든 요소 없이 콘텐츠 페이지부터 만듭니다. 이 경우 하지만 변환 대상 독립 실행형 페이지 하나 이므로 약간의 정리 레이아웃을 사용 합니다.

완료 되 면는 *Movies.cshtml* 페이지는 다음과 같습니다.

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>레이아웃 테스트

이제 레이아웃의 모양을 볼 수 있습니다. WebMatrix에서 마우스 오른쪽 단추로 클릭는 *Movies.cshtml* 페이지로 돌아간 후 선택 **브라우저에서 시작**합니다. 브라우저 페이지를 표시 하는 경우이 페이지를 같습니다.

![동영상 페이지 레이아웃을 사용 하 여 렌더링](layouts/_static/image6.png)

ASP.NET은 병합에 Movies.cshtml 페이지의 콘텐츠는  *\_Layout.cshtml* 페이지 오른쪽 위치는 `RenderBody` 메서드는 합니다. 물론 및는  *\_Layout.cshtml* 페이지 참조는 *.css* 페이지의 모양을 정의 하는 파일입니다.

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>AddMovie 페이지 레이아웃을 사용 하려면 업데이트

레이아웃의 실제 이점은 사용할 수 있는 이러한 모든 페이지에 대 한 사이트에서입니다. 열기는 *AddMovie.cshtml* 페이지.

있습니다 수 있다는 점을 잘 알고는 *AddMovie.cshtml* 페이지 원래에 게 일부 CSS 규칙의 유효성 검사 오류 메시지의 모양을 정의 하는 것입니다. 했으므로 *.css* 지금 사이트에 대 한 파일, 이러한 규칙을 이동할 수 있습니다는 *.css* 파일입니다. 제거는 *AddMovie.cshtml* 파일의 맨 아래에 추가 하는 *Movies.css* 파일입니다. 다음 규칙 이동 하는:

[!code-css[Main](layouts/samples/sample6.css)]

같은 종류의 변경 내용 확인 *AddMovie.cshtml* 에 대 한 사용 하 던 *Movies.cshtml* -추가 `Layout="~/_Layout.cshtml;` 는 불필요 한 이제는 HTML 태그를 제거 합니다. 변경 된 `<h1>` 요소의 `<h2>`합니다. 완료 되 면 페이지는이 예제와 같습니다.

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

페이지를 실행 합니다. 이제이 그림과 같이 표시 됩니다.

![동영상 추가' 페이지 레이아웃을 사용 하 여 렌더링](layouts/_static/image7.png)

사이트의 페이지에 대 한 유사한 변경 하려는- *EditMovie.cshtml* 및 *DeleteMovie.cshtml*합니다. 그러나, 수행 하기 전에 또 다른 변경 좀 더 융통성이 레이아웃을 만들 수 있습니다.

## <a name="passing-title-information-to-the-layout-page"></a>레이아웃 페이지에 제목 정보 전달

 *\_Layout.cshtml* 만든 페이지에는 `<title>` "내 동영상 사이트"로 설정 된 요소입니다. 대부분의 브라우저 탭에 텍스트와이 요소의 내용 표시:

![페이지의 &lt;제목&gt; 브라우저 탭에 표시 된 요소](layouts/_static/image8.png)

이 제목 정보는 제네릭입니다. 제목 텍스트를 현재 페이지에 더 구체적인 한다고 가정 합니다. (제목 텍스트는 검색 엔진에서 확인 하는 데도 페이지에 표시 되는 것입니다.) 와 같은 콘텐츠 페이지에서 정보를 전달할 수 *Movies.cshtml* 또는 *AddMovie.cshtml* 레이아웃 페이지 및 사용 하 여 해당 정보를 레이아웃 페이지를 사용자 지정 렌더링 합니다.

열기는 *Movies.cshtml* 페이지를 다시 합니다. 맨 위에 있는 코드에서 다음 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page` 개체는 모두에서 사용할 수 있는 *.cshtml* 페이지 이며이 작업을 위해 즉 페이지와 레이아웃 간에 정보를 공유 합니다.

열기는*\_Layout.cshtml* 페이지. 변경 된 `<title>` 요소를이 태그 같이 되도록 합니다.

[!code-html[Main](layouts/samples/sample9.html)]

이 코드에는 렌더링 된 `Page.Title` 속성 페이지에서 해당 위치에서 바로 합니다.

실행 된 *Movies.cshtml* 페이지. 이 현재 브라우저 탭이 표시의 값으로 전달 된 `Page.Title`:

![동적으로 만든 제목이 표시 브라우저 탭](layouts/_static/image9.png)

원하는 경우 브라우저에서 페이지 소스를 봅니다. 확인할 수 있습니다는 `<title>` 요소가로 렌더링 `<title>List Movies</title>`합니다.

> [!TIP] 
> 
> **Page 개체**
> 
> 유용한 특징 중 `Page` 동적 개체는-는 `Title` 속성은 고정 또는 예약 된 이름이 아닙니다. 사용할 수 있습니다 *모든* 의 값에 대 한 이름는 `Page` 개체입니다. 예를 들어 수를 쉽게 전달한 제목을 라는 속성을 사용 하 여 `Page.CurrentName` 또는 `Page.MyPage`합니다. 유일한 제한 사항은 이름 속성 이름을 지정할 수에 대 한 일반 규칙을 준수 해야 한다는 것입니다. (예를 들어 이름에는 공백입니다.)
> 
> 사용 하 여 원하는 수의 값을 전달할 수 있습니다는 `Page` 개체입니다. 레이아웃 페이지에 동영상 정보를 전달 하려는 경우 다음과 같이 사용 하 여 값을 전달할 수 있습니다 `Page.MovieTitle` 및 `Page.Genre` 및 `Page.MovieYear`합니다. (또는 다른 이름 정보를 저장할 발명에.) 유일한 요구 사항은-는 아마도 분명 한 것은-콘텐츠 페이지와 페이지 레이아웃 페이지의 동일한 이름을 사용할 수 있는입니다.
> 
> 사용 하 여 전달 되는 정보는 `Page` 개체를 레이아웃 페이지에 표시할 텍스트만으로 제한 되지 않습니다. 레이아웃 페이지에는 값을 전달할 수 있습니다 및 레이아웃 페이지의 코드 페이지의 부분을 표시 하려면 여부를 결정할 값을 사용할 수 다음 어떤 *.css* 파일을 사용 하려면 등에입니다. 에 전달 하는 값은 `Page` 개체는 다른 모든 값과 같은 코드에서 사용 하 합니다. 값 콘텐츠 페이지에서 시작 하 고 페이지 레이아웃 페이지에 전달 되는 합니다.


열기는 *AddMovie.cshtml* 페이지 제목을 제공 하는 코드의 위쪽에 선을 추가 하 고는 *AddMovie.cshtml* 페이지:

[!code-csharp[Main](layouts/samples/sample10.cs)]

실행 된 *AddMovie.cshtml* 페이지. 새 제목을 표시 됩니다.

![동적으로 만든 추가 동영상 제목이 표시 브라우저 탭](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>레이아웃을 사용 하 여 나머지 페이지를 업데이트 합니다.

이제 새 레이아웃을 사용할 수 있도록 사이트의 나머지 페이지를 마칠 수 있습니다. 열기 *EditMovie.cshtml* 및 *DeleteMovie.cshtml* 에 설정 하 고 각각에 동일한 변경 내용을 확인 합니다.

레이아웃 페이지에 연결 하는 코드 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample11.cs)]

페이지의 제목을 설정 하는 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample12.cs)]

또는

[!code-csharp[Main](layouts/samples/sample13.cs)]

불필요 한 모든 HTML 태그 제거-기본적으로, 내부에 있는 비트만 둡니다는 `<body>` 요소 (및 맨 위에 있는 코드 블록).

변경 된 `<h1>` 요소는 `<h2>` 요소입니다.

이러한 변경 내용을 수행 했으면, 테스트 실행 하 고 제대로 표시 된 대로, 그리고 제목이 올바른지 확인 합니다.

## <a name="parting-thoughts-about-layout-pages"></a>레이아웃 페이지에 대 한 분할 생각

이 자습서에서 만든는  *\_Layout.cshtml* 페이지를 사용 하는 `RenderBody` 메서드를 다른 페이지의에서 콘텐츠를 병합 합니다. 웹 페이지의 레이아웃을 사용 하기 위한 기본 패턴입니다.

레이아웃 페이지는 여기 다룰 하지 않은 추가 기능도 제공 합니다. 예를 들어, 레이아웃 페이지를 중첩할 수 있습니다-한 레이아웃 페이지를 참조할 수 다른 합니다. 중첩 된 레이아웃 다양 한 레이아웃을 필요로 하는 사이트의 하위 섹션으로 작업 하는 경우에 유용할 수 있습니다. 추가 메서드를 사용할 수도 있습니다 (예를 들어 `RenderSection`) 명명 된 레이아웃 페이지의 섹션을 설치 합니다.

레이아웃 페이지의 조합 및 *.css* 파일은 강력 합니다. 다음 자습서 시리즈의 하겠지만 WebMatrix에서 만들 수 있습니다에 기반 하는 사이트는 *템플릿*, 있는 사이트를 제공 하는 미리 작성 된 기능입니다. 서식 파일의 레이아웃 페이지 및 CSS를 보기 좋게 있고 메뉴와 같은 기능 사이트를 만들 적절 하 게 사용을 확인 합니다. 레이아웃 페이지 및 CSS를 사용 하는 기능을 보여 주는 하는 템플릿을 기반으로 하는 사이트에서 홈 페이지의 스크린 샷을 다음과 같습니다.

![헤더, 탐색 영역, 콘텐츠 영역, 선택적 섹션 및 로그인 링크를 표시 하는 WebMatrix 사이트 템플릿으로 만든 레이아웃](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>동영상 페이지 (페이지 레이아웃을 사용 하도록 업데이트)에 대 한 전체 목록을 보려면

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>완료 페이지에 대 한 목록 추가 (레이아웃에 대 한 업데이트) 동영상 페이지

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>전체 삭제 동영상 페이지 (레이아웃에 대 한 업데이트)에 대 한 목록 페이지

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>전체 편집 동영상 페이지 (레이아웃에 대 한 업데이트)에 대 한 목록 페이지

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서에서는 사람이 볼 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다.

## <a name="additional-resources"></a>추가 리소스

- [일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkID=202891) -레이아웃 작업에 더 자세히 제공 하는 문서입니다. 또한를 표시 하거나 숨기는 콘텐츠 일부가 레이아웃 페이지에는 값을 전달 하는 방법을 설명 합니다.
- [중첩 된 Razor 사용한 레이아웃 페이지](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) -Mike Brind 블로그 레이아웃 페이지를 중첩 하는 방법의 예입니다. (페이지의 다운로드 포함).

>[!div class="step-by-step"]
[이전](deleting-data.md)
[다음](publishing.md)
