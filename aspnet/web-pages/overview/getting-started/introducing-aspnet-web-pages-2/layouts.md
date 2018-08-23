---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET 웹 페이지 소개-일관적인 레이아웃 만들기 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 ASP.NET 웹 페이지를 사용 하는 사이트에서 페이지에 일관 된 모양을 만들려면 레이아웃을 사용 하는 방법을 보여 줍니다. 완료 했다고 가정 하는 중...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 8f3d9e8a6f6a0179224e18faf11db3dc1510a095
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838738"
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET 웹 페이지 소개-일관적인 레이아웃 만들기
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 사용 하는 방법을 보여 줍니다 *레이아웃* ASP.NET 웹 페이지를 사용 하는 사이트에서 페이지에 일관 된 모양을 만들려고 합니다. 통해 시리즈를 완료 했다고 가정 하 [ASP.NET 웹 페이지에서 데이터베이스 데이터 삭제](https://go.microsoft.com/fwlink/?LinkId=251584)합니다.
> 
> 학습할 내용:
> 
> - 레이아웃 페이지가 됩니다.
> - 동적 콘텐츠가 포함 된 레이아웃 페이지를 결합 하는 방법입니다.
> - 레이아웃 페이지에 값을 전달 하는 방법입니다.


## <a name="about-layouts"></a>레이아웃 정보

지금까지 만든 페이지는 모두 완료 되었습니다 독립 실행형 페이지입니다. 모두 동일한 사이트에 속하지만 되지 않은 모든 공통 요소 또는 표준 모양입니다.

대부분의 사이트에 일관 된 모양과 레이아웃 합니다. 예를 들어, 이동 하는 경우는 [Microsoft.com/web](https://www.microsoft.com/web/) 사이트 및 살펴보겠습니다, 모든 페이지는 전체 레이아웃에 시각적 테마 준수는 참조 하세요.

![헤더, 탐색 영역에서 콘텐츠 영역 및 바닥글의 레이아웃을 보여 주는 Microsoft.com/web 사이트 페이지](layouts/_static/image1.png)

*비효율적인* 이 레이아웃을 만드는 방법, 탐색 모음 머리글과 바닥글을 각 페이지에 개별적으로 정의 하는 것입니다. 하는 복제에서 동일한 태그 때마다 합니다. 변경 하려는 경우 (예: 바닥글 업데이트) 각 페이지를 개별적으로 변경 해야 합니다.

즉 *레이아웃 페이지* 제공 합니다. ASP.NET 웹 페이지에서 사이트에 있는 페이지에 대 한 전체 컨테이너를 제공 하는 레이아웃 페이지를 정의할 수 있습니다. 예를 들어, 레이아웃 페이지, 탐색 영역에서 머리글과 바닥글을 포함할 수 있습니다. 레이아웃 페이지 주요 내용 중단 되는 자리 표시자를 포함 합니다.

다음 태그 및 코드 페이지만 포함 하는 개별 콘텐츠 페이지를 정의할 수 있습니다. 콘텐츠 페이지 않아도 전체 HTML 페이지입니다. 필요가 없어도 `<body>` 요소입니다. 레이아웃 페이지의 콘텐츠를 표시 하려면 ASP.NET에 지시 하는 코드 줄을 수도 있습니다. 다음은이 관계의 작동 원리를 대략적으로 보여 주는 그림이입니다.

![두 콘텐츠 페이지와 들어갈 있는 레이아웃 페이지를 보여 주는 개념 다이어그램](layouts/_static/image2.png)

이 상호 작용 작업에 표시 되 면를 이해 하기 쉽습니다. 이 자습서에서는 레이아웃을 사용 하 여 영화 페이지를 변경 합니다.

## <a name="adding-a-layout-page"></a>레이아웃 페이지 추가

머리글, 바닥글 및 주요 내용에 대 한 영역을 사용 하 여 일반적인 페이지 레이아웃을 정의 하는 레이아웃 페이지를 만들어 시작 합니다. WebPagesMovies 사이트 라는 CSHTML 페이지 추가  *\_Layout.cshtml*합니다.

선행 밑줄 ( `_` ) 문자는 중요 합니다. 페이지의 이름을 밑줄로 시작 하는 경우 ASP.NET 브라우저에 해당 페이지를 직접 보내지 않습니다. 이 규칙은 사이트에 대 한 필요 없지만 사용자가 직접 요청할 수 있는 페이지를 정의할 수 있습니다.

페이지의 콘텐츠를 다음으로 바꿉니다.

[!code-html[Main](layouts/samples/sample1.html)]

이 태그는를 사용 하는 HTML만 볼 수 있듯이 `<div>` 보다 1을 더한 페이지에서 세 가지 섹션을 정의 하는 요소 `<div>` 세 가지 섹션이 포함 될 요소입니다. Razor 코드의 비트를 포함 하는 바닥글: `@DateTime.Now.Year`에 페이지의 위치에 있는 현재 연도 렌더링 합니다.

명명 된 스타일 시트에 대 한 링크는 *Movies.css*합니다. 스타일 시트 요소의 물리적 레이아웃의 세부 정보 정의 되는 합니다. 잠시 후에 만들어야 합니다.

이 독특한 기능  *\_Layout.cshtml* 페이지를 `@Render.Body()` 줄. 이 레이아웃은 다른 페이지와 병합 될 때 콘텐츠 어디 자리 표시자입니다.

## <a name="adding-a-css-file"></a>.Css 파일 추가

페이지의 실제 배열과 (즉, 모양) 요소를 정의 하는 기본 방법은 연계 스타일 시트 (CSS) 규칙을 사용 하는 것입니다. 만들어야 하므로 *.css* 새 레이아웃에 대 한 규칙 파일입니다.

WebMatrix에서 사이트의 루트를 선택 합니다. 그런 다음 합니다 **파일** 탭 리본의 아래의 화살표를 클릭 합니다 **새로 만들기** 단추를 클릭 **새 폴더**합니다.

![리본에서 새로 만들기 ' 새 폴더 옵션입니다.](layouts/_static/image3.png)

새 폴더의 이름을 *스타일*합니다.

![새 폴더 '스타일' 이름 지정](layouts/_static/image4.png)

새 내부 *스타일* 폴더에 파일을 만듭니다 *Movies.css*.

![새 Movies.css 파일 만들기](layouts/_static/image5.png)

새 내용을 바꿉니다 *.css* 다음 파일:

[!code-css[Main](layouts/samples/sample2.css)]

이러한 CSS 규칙에 두 가지 사항을 제외 하 고 자세히 자세하게 다루지 합니다. 하나는 글꼴과 크기로 설정 하는 것 외에도 규칙을 사용 하 여 절대 위치 머리글, 바닥글 및 메인 콘텐츠 영역 위치를 설정입니다. 경우 CSS에 배치 하는 데 익숙하지, 읽을 수 있습니다 합니다 [CSS 위치 설정을](http://www.w3schools.com/css/css_positioning.asp) W3Schools 사이트의 자습서입니다.

또 다른 사항은 개별적으로 정의 아래에 복사가 원래 되는 스타일 규칙은는 *Movies.cshtml* 파일입니다. 이러한 규칙에 사용 된 합니다 [데이터 표시에서 사용 하 여 ASP.NET 웹 페이지 소개](https://go.microsoft.com/fwlink/?LinkId=251580) 있도록 자습서는 `WebGrid` 도우미 테이블에 줄무늬를 추가 하는 태그를 렌더링 합니다. (사용 하려는 경우는 *.css* 파일 스타일 정의 될 수 있습니다도 기록 하는 전체 사이트에 대 한 스타일 규칙입니다.)

## <a name="updating-the-movies-file-to-use-the-layout"></a>레이아웃을 사용 하 여 영화 파일 업데이트

이제 새 레이아웃을 사용 하 여 사이트의 기존 파일을 업데이트할 수 있습니다. 엽니다는 *Movies.cshtml* 파일입니다. 맨 위에 있는 코드의 첫 번째 줄으로 다음을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample3.cs)]

페이지는 이제이 방법으로 시작합니다.

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

이 한 줄의 코드를 ASP.NET에 지시 때 합니다 *영화* 페이지 실행을 사용 하 여 병합 해야 합니다  *\_Layout.cshtml* 파일입니다.

있으므로 합니다 *Movies.cshtml* 파일에는 이제 레이아웃 페이지 사용에서 태그를 제거할 수 있습니다는 *Movies.cshtml* 에서 처리에 페이지를  *\_Layout.cshtml*파일입니다. 사용 합니다 `<!DOCTYPE>`, `<html>`, 및 `<body>` 태그 및 닫는 태그입니다. 전체를 꺼내서 `<head>` 요소 및 해당 규칙에 있으므로 이제 되므로 표에서 대 한 스타일 규칙을 포함 하는 해당 콘텐츠를 *.css* 파일입니다. 에 머무르 시는 동안 기존 변경 `<h1>` 요소를 `<h2>` 요소; 해야는 `<h1>` 이미 레이아웃 페이지의 요소입니다. 변경 된 `<h2>` 텍스트 "영화 목록"입니다.

일반적으로 콘텐츠 페이지에 변경이 내용을 확인 하지 않습니다. 해야 합니다. 레이아웃 페이지를 사용 하 여 사이트를 시작 하는 경우 이러한 모든 요소 없이 콘텐츠 페이지를 만듭니다. 이 경우를 변환 하는 독립 실행형 페이지 일종의 정리 이므로 레이아웃을 사용 하는 것입니다.

완료 되 면 하는 경우는 *Movies.cshtml* 페이지는 다음과 같이 표시 됩니다.

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>레이아웃 테스트

이제 레이아웃의 모양을 볼 수 있습니다. WebMatrix에서 마우스 오른쪽 단추로 클릭 합니다 *Movies.cshtml* 선택한 페이지 **브라우저에서 시작**합니다. 브라우저 페이지를 표시 하는 경우이 페이지를 같습니다.

![레이아웃을 사용 하 여 렌더링 하는 동영상 페이지](layouts/_static/image6.png)

ASP.NET은에 Movies.cshtml 페이지의 콘텐츠를 병합 합니다  *\_Layout.cshtml* 오른쪽 페이지를 `RenderBody` 메서드는. 그리고 물론 합니다  *\_Layout.cshtml* 참조 페이지를 *.css* 페이지의 모양을 정의 하는 파일입니다.

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>레이아웃을 사용 하 여 AddMovie 페이지를 업데이트 하는 중

레이아웃의 진정한 이점이 사용할 수 있는 이러한 모든 페이지에 대 한 사이트의 경우 엽니다는 *AddMovie.cshtml* 페이지입니다.

있습니다 수에 유의 해야 합니다 *AddMovie.cshtml* 페이지 있던 일부 CSS 규칙 유효성 검사 오류 메시지의 모양을 정의 하 합니다. 했으므로 *.css* 지금 사이트에 대 한 파일을 해당 규칙을 이동할 수 있습니다 합니다 *.css* 파일입니다. 제거 된 *AddMovie.cshtml* 파일의 맨 아래에 추가 하는 *Movies.css* 파일입니다. 다음 규칙을 이동 하는:

[!code-css[Main](layouts/samples/sample6.css)]

이제 동일한 종류의 변경 내용을 확인 하십시오 *AddMovie.cshtml* 는 *Movies.cshtml* -추가 `Layout="~/_Layout.cshtml;` 및 불필요 한 이제는 HTML 태그를 제거 합니다. 변경 된 `<h1>` 요소를 `<h2>`입니다. 완료 되 면 페이지는이 예제와 같이 표시 됩니다.

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

페이지를 실행 합니다. 이제이 그림과 같이 표시 됩니다.

![레이아웃을 사용 하 여 렌더링 하는 영화 추가 페이지](layouts/_static/image7.png)

사이트의 페이지에 대 한 유사한 변경 하려는 — *EditMovie.cshtml* 하 고 *DeleteMovie.cshtml*합니다. 그러나를 수행 하기 전에 할 수 있습니다 다른 변경 하기가 좀 더 유연한 레이아웃.

## <a name="passing-title-information-to-the-layout-page"></a>레이아웃 페이지 제목 정보 전달

합니다  *\_Layout.cshtml* 사용자가 만든 페이지에는 `<title>` "내 동영상 사이트"로 설정 된 요소입니다. 대부분의 브라우저 탭의 텍스트와이 요소의 콘텐츠를 표시:

![페이지의 &lt;title&gt; 브라우저 탭에 표시 된 요소](layouts/_static/image8.png)

이 제목 정보는 제네릭입니다. 현재 페이지에 더 정확 하 게 하는 제목 텍스트 한다고 가정해 보겠습니다. (제목 텍스트도 사용 됩니다 검색 엔진에 대 한 페이지 결정.) 와 같은 콘텐츠 페이지 로부터 정보를 전달할 수 있습니다 *Movies.cshtml* 하거나 *AddMovie.cshtml* 레이아웃 페이지를 사용 하 여 해당 정보를 레이아웃 페이지를 사용자 지정 렌더링 합니다.

엽니다는 *Movies.cshtml* 페이지를 다시 합니다. 맨 위에 있는 코드에서 다음 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample8.cs)]

합니다 `Page` 개체가 모두에서 사용할 수 있습니다 *.cshtml* 페이지 이며이 위해 namely 페이지 및 해당 레이아웃 간에 정보를 공유 합니다.

엽니다는<em>\_Layout.cshtml</em> 페이지입니다. 변경 된 `<title>` 요소 하므로이 태그는 다음과 같습니다.

[!code-html[Main](layouts/samples/sample9.html)]

이 코드에 렌더링 된 `Page.Title` 속성 페이지에서 해당 위치에서 오른쪽입니다.

실행 합니다 *Movies.cshtml* 페이지입니다. 이 이번 브라우저 탭에 표시 값으로 전달 된 `Page.Title`:

![동적으로 만든 제목을 표시 하는 브라우저 탭](layouts/_static/image9.png)

원한다 면 브라우저에서 페이지 소스를 봅니다. 볼 수 있습니다는 `<title>` 요소는 렌더링 `<title>List Movies</title>`합니다.

> [!TIP] 
> 
> **Page 개체**
> 
> 유용한 특징 중 하나 `Page` 동적 개체는-는 `Title` 속성은 고정 또는 예약 된 이름이 아닙니다. 사용할 수 있습니다 *모든* 의 값에 대 한 이름를 `Page` 개체입니다. 예를 들어, 수를 쉽게 전달한 제목 라는 속성을 사용 하 여 `Page.CurrentName` 또는 `Page.MyPage`합니다. 단, 이름을 지정할 수 있는 속성에 대 한 일반 규칙을 따르도록 이름입니다. (예를 들어 이름에는 공백입니다.)
> 
> 사용 하 여 원하는 수의 값을 전달할 수 있습니다는 `Page` 개체입니다. 레이아웃 페이지에 동영상 정보를 전달 하려는 경우와 같이 사용 하 여 값을 전달할 수 있습니다 `Page.MovieTitle` 하 고 `Page.Genre` 고 `Page.MovieYear`입니다. (또는 정보를 저장할 고안 하는 다른 모든 이름입니다.) 유일한 요구 사항은-는 아마도 명백한-콘텐츠 페이지와 레이아웃 페이지에 동일한 이름을 사용 해야 합니다.
> 
> 사용 하 여 전달 되는 정보는 `Page` 개체만 표시할 텍스트를 레이아웃 페이지에서 제한 되지 않습니다. 레이아웃 페이지에서 값을 전달할 수 있으며 레이아웃 페이지의 코드 페이지의 섹션 표시 여부를 결정 하는 값을 사용할 수 다음 무엇 *.css* 를 사용 하려면 파일 등에입니다. 에 전달할 값을 `Page` 개체는 다른 값 처럼 코드에서 사용 합니다. 값 콘텐츠 페이지에서 시작 하 고 레이아웃 페이지에 전달 되는 죠.


엽니다는 *AddMovie.cshtml* 페이지 및 제목을 제공 하는 코드의 위쪽에 선을 추가 합니다 *AddMovie.cshtml* 페이지:

[!code-csharp[Main](layouts/samples/sample10.cs)]

실행 합니다 *AddMovie.cshtml* 페이지입니다. 새 제목을 표시 됩니다.

![표시 추가 영화 제목을 동적으로 생성 하는 브라우저 탭](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>레이아웃을 사용 하 여 나머지 페이지를 업데이트 하는 중

이제 새 레이아웃을 사용할 수 있도록 사이트의 나머지 페이지를 마칠 수 있습니다. 오픈 *EditMovie.cshtml* 하 고 *DeleteMovie.cshtml* 에 설정 하 고 각각에 동일한 변경 합니다.

레이아웃 페이지에 연결 하는 코드 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample11.cs)]

페이지의 제목을 설정 하는 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample12.cs)]

또는

[!code-csharp[Main](layouts/samples/sample13.cs)]

불필요 한 모든 HTML 태그 제거-기본적으로 내에 있는 비트만 유지 합니다 `<body>` 요소 (및 맨 위에 있는 코드 블록).

변경 된 `<h1>` 요소는 `<h2>` 요소입니다.

이러한 변경 내용, 변경한 경우 각 테스트를 올바르게 표시 되 고 제목 올바른지 확인 합니다.

## <a name="parting-thoughts-about-layout-pages"></a>레이아웃 페이지에 대 한 분할 고려 사항

만든이 자습서는  *\_Layout.cshtml* 페이지를 사용 하는 `RenderBody` 다른 페이지에서 콘텐츠를 병합 하는 방법. 웹 페이지의 레이아웃을 사용 하기 위한 기본 패턴입니다.

레이아웃 페이지에 여기서는 다루지 않음는 추가 기능이 있습니다. 예를 들어, 레이아웃 페이지를 중첩할 수 있습니다-한 레이아웃 페이지 다른 참조에 있습니다. 중첩 된 레이아웃 다른 레이아웃을 필요로 하는 사이트의 하위 섹션을 사용 하 여 작업 하는 경우에 유용할 수 있습니다. 추가 메서드를 사용할 수도 있습니다 (예를 들어 `RenderSection`)를 설정 하 라는 레이아웃 페이지의 섹션입니다.

레이아웃 페이지의 조합 하 고 *.css* 파일 보다 강력 합니다. 다음 자습서 시리즈에서 살펴보겠지만 WebMatrix에서 만들 수 있습니다를 기반으로 하는 사이트를 *템플릿*, 된 사이트를 제공 하는 미리 작성 된 기능. 템플릿은은 레이아웃 페이지 및 CSS는 훌륭해 있고 기능 메뉴와 같은 사이트를 만드는 데 적절 하 게 사용을 확인 합니다. 레이아웃 페이지 및 CSS를 사용 하는 기능을 표시 하는 템플릿을 기반으로 하는 사이트에서 홈 페이지의 스크린샷은 다음과 같습니다.

![헤더, 탐색 영역에서 콘텐츠 영역, 선택적인 섹션 및 로그인 링크를 표시 하는 WebMatrix 사이트 템플릿으로 만든 레이아웃](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>동영상 페이지 (레이아웃 페이지를 사용 하도록 업데이트)에 대 한 전체 목록

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>완료 페이지에 대 한 목록 추가 (레이아웃에 맞게 업데이트) 동영상 페이지

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>전체 삭제 동영상 페이지 (레이아웃에 맞게 업데이트)에 대 한 페이지 목록

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>전체 편집 동영상 페이지 (레이아웃에 맞게 업데이트)에 대 한 페이지 목록

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>다음에 나오는

다음 자습서 인 사람이 볼 수 있도록 사이트를 인터넷에 게시 하는 방법에 알아봅니다.

## <a name="additional-resources"></a>추가 리소스

- [일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkID=202891) -레이아웃 작업에 몇 가지 자세한 내용을 제공 하는 문서입니다. 레이아웃 페이지를 표시 하거나 숨기는 콘텐츠의 일부 값을 전달 하는 방법을 설명 합니다.
- [중첩 된 레이아웃 페이지 Razor 사용한](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) -Mike Brind 블로그 레이아웃 페이지를 중첩 하는 방법의 예입니다. (페이지의 다운로드를 포함 합니다.)

> [!div class="step-by-step"]
> [이전](deleting-data.md)
> [다음](publishing.md)
