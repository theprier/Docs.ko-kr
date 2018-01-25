---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: "마스터 페이지 (C#)의 Url | Microsoft Docs"
author: rick-anderson
description: "마스터 페이지의 Url이 디렉터리는 콘텐츠 페이지와 다른 상대에 마스터 페이지 파일이 손상 될 수 있습니다 어떻게 해결 합니다. 기준 주소 확인 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2008
ms.topic: article
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b01f0ac780121c4e0941df6016220a1cb1ed2d1
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="urls-in-master-pages-c"></a>마스터 페이지 (C#)의 Url
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> 마스터 페이지의 Url이 디렉터리는 콘텐츠 페이지와 다른 상대에 마스터 페이지 파일이 손상 될 수 있습니다 어떻게 해결 합니다. 통해 Url의 기준 주소에 ~ 선언적 구문 및 ResolveUrl 및 ResolveClientUrl를 프로그래밍 방식으로 사용 합니다. (또한 살펴보기


## <a name="introduction"></a>소개

모든 예제에서 살펴본 지금까지 마스터 및 콘텐츠 페이지 (웹 사이트의 루트 폴더)와 동일한 폴더에 있는 있어야 합니다. 하지만 마스터 및 콘텐츠 페이지 같은 폴더에 있어야는 이유 이유가 없습니다. 대부분 하위 폴더에 있는 콘텐츠 페이지를 만들 수 있습니다. 마찬가지로, 만들 수는 `~/MasterPages/` 폴더 사이트의 마스터 페이지를 배치 하는 위치입니다.

다른 폴더에 마스터 및 콘텐츠 페이지를 배치 잠재적인 문제 하나는 끊어진된 Url에 포함 됩니다. 하이퍼링크, 이미지 또는 기타 요소에는 상대 Url을 포함 하는 마스터 페이지, 링크 다른 폴더에 있는 콘텐츠 페이지에 대해 잘못 됩니다. 이 자습서에서는이 문제는 물론 해결 방법의 소스를 살펴보겠습니다.

## <a name="the-problem-with-relative-urls"></a>상대 Url 관련 문제

웹 페이지에 대 한 URL를 라고는 *상대 URL* 를 가리키는 리소스의 위치는 웹 사이트의 폴더 구조에서 웹 페이지의 위치를 기준으로 하는 경우. 선행 슬래시로 시작 되지 않는 모든 URL (`/`) 또는 프로토콜 (같은 `http://`)는 브라우저 URL을 포함 하는 웹 페이지의 위치에 기반 하 여 자동적으로 해결 되므로 때문에 상대적입니다.

예를 들어 웹 사이트에는 `~/Images/` 단일 이미지 파일, 폴더 `PoweredByASPNET.gif`합니다. 마스터 페이지 파일 `Site.master` 에 `<img>` 요소에는 `footerContent` 다음 태그를 사용 하 여 영역:


[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

`src` 특성 값에는 `<img>` 로 시작 하지 않는 때문에 요소는 상대 URL `/` 또는 `http://`합니다. 즉,는 `src` 특성 값은 브라우저 찾는 위치를 지정 된 `Images` 라는 파일에 대 한 하위 폴더 `PoweredByASPNET.gif`합니다.

콘텐츠 페이지를 방문 하는 위의 태그 브라우저에 직접 전송 됩니다. 방문을 `About.aspx` 브라우저에 보내지는 HTML 소스를 확인 합니다. 마스터 페이지에는 실제 같은 태그는 브라우저에 보내지는 찾을 수 있습니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

콘텐츠 페이지 루트 폴더에 있으면 (그대로 `About.aspx`) 있기 때문에 예상 대로 작동 하는 것는 `Images` 루트 폴더에 상대적인 하위 폴더입니다. 그러나 작업 분해 콘텐츠 페이지 마스터 페이지와 다른 폴더에 있으면 합니다. 이 설명 하기 라는 하위 폴더를 만들 `Admin`합니다. 다음으로 명명 된 콘텐츠 페이지를 추가 `Default.aspx` 에 `Admin` 새 페이지를 바인딩할 수 있도록 폴더는 `Site.master` 마스터 페이지입니다.

> [!NOTE]
> 에 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 라는 기본 페이지를 사용자 지정 클래스 만든 자습서 `BasePage` 콘텐츠 페이지의 제목을 자동으로 설정 하는 (경우 것 하지 명시적으로 할당) 됩니다. 파생 되는 새로 만든된 페이지의 코드 숨김 클래스에 반드시 `BasePage` 이 기능을 활용할 수 있도록 합니다.


이 콘텐츠 페이지를 만든 후 솔루션 탐색기는 그림 1을 비슷하게 나타납니다.


![새 폴더 및 ASP.NET 페이지 프로젝트에 추가 되었습니다.](urls-in-master-pages-cs/_static/image1.png)

**그림 01**: 새 폴더 및 ASP.NET 페이지 프로젝트에 추가 되었습니다


다음을 업데이트 하는 `Web.sitemap` 포함 되도록 새 파일을 `<siteMapNode>` 이 단원에 대 한 항목입니다. 다음 XML 표시 전체 `Web.sitemap` 제 3의 추가 포함 되어 있는 태그 `<siteMapNode>` 요소입니다.


[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

새로 만든 `Default.aspx` 페이지에 해당 하에서 4 개의 contentplaceholders의 네 가지 콘텐츠 컨트롤 있어야 `Site.master`합니다. 일부 텍스트를 참조 하는 콘텐츠 컨트롤 추가 `MainContent` ContentPlaceHolder 한 후 브라우저를 통해 페이지를 방문 합니다. 그림 2에서 볼 수 있듯이 브라우저를 찾을 수 없습니다는 `PoweredByASPNET.gif` 이미지 파일입니다. 여기에 무슨 일이 일어나고 있나요?

`~/Admin/Default.aspx` 콘텐츠 페이지에 대 한 동일한 HTML 보내집니다는 `footerContent` 영역으로는 `About.aspx` 페이지:


[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

때문에 `<img>` 요소의 `src` 특성은 상대 URL을 브라우저에 대 한 조회 하려고는 `Images` 폴더는 웹 페이지의 폴더 위치를 기준으로 합니다. 브라우저에서 이미지 파일을 찾고 즉, `Admin/Images/PoweredByASPNET.gif`합니다.


[![PoweredByASPNET.gif 이미지 파일을 찾을 수 없습니다.](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**그림 02**:는 `PoweredByASPNET.gif` 이미지 파일을 찾을 수 없습니다 ([전체 크기 이미지를 보려면 클릭](urls-in-master-pages-cs/_static/image4.png))


### <a name="replacing-relative-urls-with-absolute-urls"></a>절대 url이 상대 Url 바꾸기

경우에 상대 URL 반대로 *절대 URL*는 슬래시로 시작 하는 1 (`/`) 또는와 같은 프로토콜 `http://`합니다. 같은 절대 URL는 알려진된 고정된 소수점에서 리소스의 위치를 지정 하는 절대 URL을 되므로 웹 사이트의 폴더 구조에서 웹 페이지의 위치에 관계 없이 모든 웹 페이지에서 유효 합니다.

그림 2에 표시 된 깨진된 이미지를 해결 하려면 업데이트 해야는 `<img>` 요소의 `src` 특성 절대 URL을 사용 하 여 상대 대신 합니다. 올바른 절대 URL을 확인 하려면 웹 사이트의 웹 페이지 중 하나를 방문 하 고 주소 표시줄을 검사 합니다. 웹 응용 프로그램의 정규화 된 경로 그림 2의 주소 표시줄에서 볼 수 있듯이 `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`합니다. 따라서 업데이트할 수 있습니다는 `<img>` 요소의 `src` 특성을 다음 두 개의 절대 Url 중 하나:

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

업데이트 하는 `<img>` 요소의 `src` 특성 위에 표시 된 형식 중 하나를 사용 하는 절대 URL을 한 후 방문 하는 `~/Admin/Default.aspx` 브라우저를 통해 페이지입니다. 이 현재 브라우저는 올바르게 찾아서 표시는 `PoweredByASPNET.gif` 이미지 파일 (그림 3 참조).


[![PoweredByASPNET.gif 이미지는 이제 표시](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**그림 03**:는 `PoweredByASPNET.gif` 이미지는 이제 표시 ([전체 크기 이미지를 보려면 클릭](urls-in-master-pages-cs/_static/image7.png))


절대 URL에서 하드 코딩 작동 하는 동안 그 밀접 하 게 결합 HTML 웹 사이트의 서버 및 폴더 위치를 변경할 수 있습니다. 폼의 절대 URL을 사용 하 여 `http://localhost:3908/...` 불안정은 때문에 포트 번호 앞 `localhost` Visual Studio의 기본 제공 ASP.NET 개발 웹 서버를 시작할 때마다 자동으로 선택 합니다. 마찬가지로,는 `http://localhost` 부분 때만 유효 로컬로 테스트 합니다. URL 기본 바뀝니다 다른 항목에 같은 코드를 프로덕션 서버에 배포 되 면 `http://www.yourserver.com`합니다. 양식에서 절대 URL `/ASPNET_MasterPages_Tutorial_04_CS/...` 도 다르므로 종종이 응용 프로그램 경로 개발 및 프로덕션 서버 간에 동일한 오류에서 발생 합니다.

좋은 소식은 ASP.NET 런타임에 유효한 상대 URL을 생성 하기 위한 메서드를 제공 한다는 것입니다.

## <a name="usingandresolveclienturl"></a>Using`~`and`ResolveClientUrl`

대신 절대 URL를 하드 코딩 보다 ASP.NET을 사용 하면 페이지 개발자가 물결표를 사용 하도록 (`~`) 웹 응용 프로그램의 루트를 나타냅니다. 예를 들어 표기법 사용이 자습서의 앞부분에 나오는 `~/Admin/Default.aspx` 을 가리키는 텍스트에는 `Default.aspx` 페이지에 `Admin` 폴더입니다. `~` 나타냅니다는 `Admin` 폴더에는 웹 응용 프로그램의 루트의 하위 폴더입니다.

`Control` 클래스의 [ `ResolveClientUrl` 메서드](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) URL을 사용 하 고는 컨트롤이 포함 된 웹 페이지에 대 한 적절 한 상대 URL을 수정 합니다. 예를 들어 호출 `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` 에서 `About.aspx` 반환 `Images/PoweredByASPNET.gif`합니다. 그러나 호출에서 `~/Admin/Default.aspx`, 반환 `../Images/PoweredByASPNET.gif`합니다.

> [!NOTE]
> 모든 ASP.NET 서버 컨트롤에서 파생 되므로 `Control` 클래스, 모든 서버 컨트롤에 액세스할 수는 `ResolveClientUrl` 메서드. 도 `Page` 클래스에서 파생 되는 `Control` 클래스, ASP.NET 페이지의 코드 숨김 클래스에서 직접이 메서드를 사용할 수 있는 의미 합니다.


### <a name="usingin-the-declarative-markup"></a>사용 하 여`~`선언적 태그에

URL 관련 속성을 포함 하는 몇 가지 ASP.NET 웹 컨트롤: 하이퍼링크 컨트롤에는 `NavigateUrl` 속성, 컨트롤에 이미지는 `ImageUrl` 속성 및 기타 등등. 이러한 컨트롤의 URL 관련 속성 값을 전달를 렌더링할 때 `ResolveClientUrl`합니다. 따라서 이러한 속성에 포함 하는 경우는 `~` 를 웹 응용 프로그램의 루트를 나타내는 URL 유효한 상대 URL 하도록 수정 됩니다.

ASP.NET 서버 컨트롤에만 변환 염두에서에 둬야는 `~` URL와 관련 된 컨트롤 속성에서입니다. 경우는 `~` 와 같은 정적 HTML 태그에 표시 `<img src="~/Images/PoweredByASPNET.gif" />`, ASP.NET 엔진 보냅니다는 `~` 나머지 HTML 콘텐츠를 함께 브라우저로 합니다. 브라우저를 가정 하는 `~` URL의 일부입니다. 예를 들어, 브라우저에 태그를 수신 하는 경우 `<img src="~/Images/PoweredByASPNET.gif" />` 라는 하위 폴더는 가정 `~` 하위 폴더와 `Images` 이미지 파일을 포함 하는 `PoweredByASPNET.gif`합니다.

이미지 태그를 수정 하려면 `Site.master`, 대체 기존 `<img>` ASP.NET 이미지 웹 컨트롤이 있는 요소입니다. 이미지 웹 컨트롤 설정 `ID` 를 `PoweredByImage`, 해당 `ImageUrl` 속성을 `~/Images/PoweredByASPNET.gif`, 및 해당 `AlternateText` "ASP.NET에서 Powered!"에 속성


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

마스터 페이지에이 변경 내용을 확인 한 후 다시 방문 하 여 `~/Admin/Default.aspx` 페이지를 다시 합니다. 이 현재는 `PoweredByASPNET.gif` 이미지 파일의 페이지에 표시 (그림 3 참조). 컨트롤은 이미지 웹으로 렌더링 될 때이 사용 하 여는 `ResolveClientUrl` 해결 방법을 해당 `ImageUrl` 속성 값입니다. `~/Admin/Default.aspx` 는 `ImageUrl` HTML 소스 프로그램의 다음 코드 조각으로 적절 한 상대 URL로 변환 됩니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> 웹 URL 기반 컨트롤 속성에 사용 될 뿐만 아니라는 `~` 호출할 때에 사용할 수는 `Response.Redirect` 및 `Server.MapPath` 다른 규칙 으로부터 메서드. 또한는 `ResolveClientUrl` 필요한 경우 ASP.NET 또는 마스터 페이지의 선언적 태그에서 직접 메서드 호출 될 수 있습니다; 참조 [Fritz 양 파형](https://www.pluralsight.com/blogs/fritz/)의 블로그 항목 [Using `ResolveClientUrl` 태그에서](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)합니다.


## <a name="fixing-the-master-pages-remaining-relative-urls"></a>마스터 페이지의 상대 Url 남은 수정

이외에 `<img>` 요소에는 `footerContent` 방금 고정, 마스터 페이지 주의 해야 하는 한 더 상대 URL을 포함 합니다. `topContent` 영역 "마스터 페이지 자습서,"를 가리키는 링크에 포함 됩니다. `Default.aspx`합니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

이 URL은 상대, 때문에 사용자를 보냅니다는 `Default.aspx` 콘텐츠 페이지를 방문 하는 것의 폴더에는 페이지입니다. 항상이 링크를 `Default.aspx` 교체 해야 하는 루트 폴더에는 `<a>` 하이퍼링크 웹 요소를 사용할 수 있도록 제어는 `~` 표기법입니다.

제거는 `<a>` 요소 태그를 제자리에 하이퍼링크 컨트롤을 추가 합니다. 하이퍼링크의 설정 `ID` 를 `lnkHome`, 해당 `NavigateUrl` 속성을 `~/Default.aspx`, 및 해당 `Text` 속성을 "마스터 페이지 자습서"


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

정말 간단하죠. 이 시점에서 모든 마스터 페이지 및 콘텐츠 페이지 폴더에 관계 없이 콘텐츠 페이지에서 렌더링 될 때 가격 마스터 페이지에 있는 Url 기반 제대로에 있습니다.

### <a name="automatic-url-resolution-in-theheadsection"></a>자동 URL 해상도`<head>`섹션

에 [ *사이트 전체 레이아웃을 사용 하 여 마스터 페이지를 만드는* ](creating-a-site-wide-layout-using-master-pages-cs.md) 추가 자습서는 `<link>` 에 `Styles.css` 파일에 `<head>` 영역:


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

반면는 `<link>` 요소의 `href` 특성은 상대 런타임에 적절 한 경로를 자동으로 변환 합니다. 설명한 것 처럼는 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서는 `<head>` 영역은 수정할 수 있는 서버측 컨트롤 실제로 렌더링 될 때 내부 컨트롤의 내용입니다.

이 확인 하려면 다시 방문 하 여 `~/Admin/Default.aspx` 페이지를 브라우저에 보내지는 HTML 소스를 볼 합니다. 아래 코드 조각에서 볼 수 있듯이 `<link>` 요소의 `href` 특성 적절 한 상대 url을 자동으로 수정 된 `../Styles.css`합니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>요약

마스터 페이지 링크, 이미지 및 URL을 통해 지정 해야 하는 기타 외부 리소스에 자주 포함 됩니다. 마스터 페이지 및 콘텐츠 페이지와 동일한 폴더에 존재 하지 않을 때문에는 상대 Url을 사용 하 여 abstain 해야 합니다. 하드 코드 된 절대 Url을 사용 하는 가능 하지만 웹 응용 프로그램의 절대 URL 결합 하므로 밀접 하 게 수행 하 합니다. 종종 될 때 처럼 이동 하거나 웹 응용 프로그램-배포의 절대 URL-변경 되 면 뒤로 돌아가서 절대 Url을 업데이트 해야 해야 합니다.

물결표를 사용 하는 이상적인 방법입니다 (`~`) 응용 프로그램 루트를 나타냅니다. URL 관련 속성을 포함 하는 ASP.NET 웹 컨트롤 매핑는 `~` 런타임에 응용 프로그램 루트에 있습니다. 내부적으로, 웹 컨트롤이 사용 하는 `Control` 클래스의 `ResolveClientUrl` 유효한 상대 URL을 생성 하는 메서드. 이 메서드는 public 및 모든 서버 컨트롤에서 사용할 수 있는 (포함 하 여는 `Page` 클래스), 있습니다 사용할 수 있도록 프로그래밍 방식으로 코드 숨김 클래스에서는 필요한 경우.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Asp.net에서 마스터 페이지](http://www.odetocode.com/Articles/419.aspx)
- [마스터 페이지의 URL 기준 주소](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [사용 하 여 `ResolveClientUrl` 태그에서](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

>[!div class="step-by-step"]
[이전](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
[다음](control-id-naming-in-content-pages-cs.md)
