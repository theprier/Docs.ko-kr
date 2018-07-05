---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: 마스터 페이지 (C#)의 Url | Microsoft Docs
author: rick-anderson
description: 마스터 페이지의 Url이 마스터 페이지 파일의 콘텐츠 페이지 이외의 다른 상대 디렉터리에 있는 것으로 인해 중단 될 수 있습니다 하는 방법을 다룹니다. 기준 주소 다시 지정 하는 방법을 살펴봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2008
ms.topic: article
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: dcbd066a55fed3dd6c79e8a091e61449f85531b0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398390"
---
<a name="urls-in-master-pages-c"></a>마스터 페이지 (C#)의 Url
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> 마스터 페이지의 Url이 마스터 페이지 파일의 콘텐츠 페이지 이외의 다른 상대 디렉터리에 있는 것으로 인해 중단 될 수 있습니다 하는 방법을 다룹니다. 통해 Url 기준 주소 다시 지정 살펴봅니다 ~ 선언적 구문 및 ResolveUrl 및 ResolveClientUrl를 프로그래밍 방식으로 사용 합니다. (또한 살펴보고


## <a name="introduction"></a>소개

모든 예제에서 살펴본 지금 동일한 폴더 (웹 사이트의 루트 폴더)에 마스터 및 콘텐츠 페이지 되었습니다. 하지만 동일한 폴더에 마스터 및 콘텐츠 페이지 해야 이유 이유가 없습니다. 확실히 하위 폴더의 콘텐츠 페이지를 만들 수 있습니다. 마찬가지로, 만들 수는 `~/MasterPages/` 폴더 사이트의 마스터 페이지를 배치 하는 위치입니다.

서로 다른 폴더에 마스터 및 콘텐츠 페이지를 배치 하는 한 가지 잠재적인 문제가 손상 된 Url에 포함 됩니다. 하이퍼링크, 이미지 또는 다른 요소에서 상대 Url을 포함 하는 마스터 페이지, 링크를 다른 폴더에 있는 콘텐츠 페이지에 대 한 유효한 됩니다. 이 자습서에서는 소스를 대안 뿐만 아니라이 문제를 살펴봅니다.

## <a name="the-problem-with-relative-urls"></a>상대 Url 사용 하 여 문제

웹 페이지의 URL 이라고는 *상대 URL* 토큰이 가리키는 리소스의 위치는 웹 사이트의 폴더 구조에서 웹 페이지의 위치를 기준으로 하는 경우. 선행 슬래시로 시작 하지 않는 모든 URL (`/`) 또는 프로토콜 (같은 `http://`) 상대 이므로 URL이 포함 된 웹 페이지의 위치를 기반으로 브라우저에서 확인 됩니다.

예를 들어 웹 사이트에는 `~/Images/` 단일 이미지 파일, 폴더 `PoweredByASPNET.gif`합니다. 마스터 페이지 파일을 `Site.master` 에 `<img>` 요소에는 `footerContent` 다음 태그를 사용 하 여 지역:


[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

합니다 `src` 특성 값을 `<img>` 요소 이므로 상대 URL로 시작 하지 않습니다 `/` 또는 `http://`합니다. 즉, 합니다 `src` 특성 값 표시 하도록 브라우저에 지시 합니다 `Images` 라는 파일에 대 한 하위 폴더 `PoweredByASPNET.gif`합니다.

콘텐츠 페이지를 방문 하는 경우 위의 태그는 브라우저에 직접 전송 됩니다. 방문을 내어 `About.aspx` 브라우저로 전송의 HTML 소스를 확인 합니다. 브라우저에 마스터 페이지의 정확히 동일한 태그를 보냈음을 찾을 수 있습니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

콘텐츠 페이지 루트 폴더에 있으면 (그대로 `About.aspx`) 있기 때문에 예상 대로 작동 하는 모든 항목을 `Images` 루트 폴더에 상대적인 하위 폴더입니다. 그러나 콘텐츠 페이지 마스터 페이지와 다른 폴더에 있으면 작업 중단 합니다. 예를 들어를 라는 하위 폴더를 만듭니다 `Admin`합니다. 다음으로 명명 된 콘텐츠 페이지를 추가 `Default.aspx` 에 `Admin` 폴더에 새 페이지에 바인딩할 수 있도록는 `Site.master` 마스터 페이지입니다.

> [!NOTE]
> 에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서 라는 기본 페이지를 사용자 지정 클래스를 만들었습니다 `BasePage` 콘텐츠 페이지의 제목을 자동으로 설정 하는 (하는 경우 해당 명시적으로 할당 되지 않았습니다)입니다. 새로 생성된 된 페이지의 코드 숨김 클래스에서 파생 해야 `BasePage` 이 기능을 활용할 수 있도록 합니다.


이 콘텐츠 페이지를 만든 후 솔루션 탐색기는 그림 1 유사 해야 합니다.


![새 폴더 및 ASP.NET 페이지 프로젝트에 추가 되었습니다.](urls-in-master-pages-cs/_static/image1.png)

**그림 01**: 새 폴더 및 ASP.NET 페이지 프로젝트에 추가 되었습니다


다음으로 업데이트 합니다 `Web.sitemap` 포함할 새 파일을 `<siteMapNode>` 이 단원에 대 한 항목입니다. 다음 XML에서는 전체를 보여 줍니다 `Web.sitemap` 이제는 제 3의 추가 포함 하는 태그 `<siteMapNode>` 요소입니다.


[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

새로 만든 `Default.aspx` 페이지에는 네 가지 콘텐츠 컨트롤에 해당 하는 네 가지 ContentPlaceHolders에서 있어야 `Site.master`합니다. 참조 하는 콘텐츠 컨트롤에 일부 텍스트를 추가 합니다 `MainContent` ContentPlaceHolder 한 후 브라우저를 통해 페이지를 방문 합니다. 그림 2에서 알 수 있듯이, 브라우저를 찾을 수 없습니다는 `PoweredByASPNET.gif` 이미지 파일입니다. 여기에 무슨 일이 일어나고 있나요?

합니다 `~/Admin/Default.aspx` 콘텐츠 페이지에 대 한 동일한 HTML 전송 되는 `footerContent` 지역 처럼를 `About.aspx` 페이지:


[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

때문에 `<img>` 요소의 `src` 특성은 상대 URL을 브라우저 표시 하려고를 `Images` 웹 페이지의 폴더 위치를 기준으로 폴더입니다. 즉, 브라우저 이미지 파일을 찾고 `Admin/Images/PoweredByASPNET.gif`합니다.


[![PoweredByASPNET.gif 이미지 파일을 찾을 수 없습니다.](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**그림 02**: 합니다 `PoweredByASPNET.gif` 이미지 파일을 찾을 수 없습니다 ([클릭 하 여 큰 이미지 보기](urls-in-master-pages-cs/_static/image4.png))


### <a name="replacing-relative-urls-with-absolute-urls"></a>절대 Url을 사용 하 여 상대 Url을으로 바꿉니다.

상대 URL의 반대 되는 *절대 URL*, 슬래시로 시작 되는 (`/`) 또는와 같은 프로토콜 `http://`합니다. 알려진된 고정된 지점에서 리소스의 위치를 지정 하는 절대 URL을 하기 때문에 같은 절대 URL을 웹 사이트의 폴더 구조에서 웹 페이지의 위치에 관계 없이 모든 웹 페이지에 유효 합니다.

그림 2 에서처럼 깨진된 이미지를 해결 하려면 업데이트 해야 합니다 `<img>` 요소의 `src` 특성 절대 URL을 상대 대신 사용할 수 있도록 합니다. 올바른 절대 URL을 확인 하려면 웹 사이트의 웹 페이지 중 하나를 방문 하 고 주소 표시줄을 검사 합니다. 웹 응용 프로그램의 정규화 된 경로 그림 2의 주소 표시줄에서 알 수 있듯이, `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`합니다. 따라서 업데이트 수를 `<img>` 요소의 `src` 특성을 다음 두 개의 절대 Url 중 하나:

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

잠시 업데이트 하는 `<img>` 요소의 `src` 위에 표시 된 형식 중 하나를 사용 하 여 절대 url 특성 및 다음 방문 하 여는 `~/Admin/Default.aspx` 브라우저를 통해 페이지입니다. 브라우저를 제대로 찾아 표시할이 이번을 `PoweredByASPNET.gif` 이미지 파일 (그림 3 참조).


[![PoweredByASPNET.gif 이미지는 이제 표시](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**그림 03**: 합니다 `PoweredByASPNET.gif` 이미지가 표시 됩니다 ([클릭 하 여 큰 이미지 보기](urls-in-master-pages-cs/_static/image7.png))


절대 URL 하드 코딩 작동 하는 동안이 밀접 하 게 결합 HTML 웹 사이트의 서버 및 폴더 위치를 변경할 수 있습니다. 폼의 절대 URL을 사용 하 여 `http://localhost:3908/...` 불안정는 때문에 위의 포트 번호를 `localhost` Visual Studio의 기본 제공 ASP.NET 개발 웹 서버를 시작할 때마다 자동으로 선택 합니다. 마찬가지로,는 `http://localhost` 파트 때만 유효 로컬로 테스트 합니다. URL 기본 바뀌어 다른 항목에 같은 코드를 프로덕션 서버로 배포 되 면 `http://www.yourserver.com`합니다. 폼의 절대 URL `/ASPNET_MasterPages_Tutorial_04_CS/...` 도 동일한 때에서 증가 하므로 문제가 발생이 응용 프로그램 경로 개발 및 프로덕션 서버 간의 다른 경우가 많습니다.

좋은 소식은 ASP.NET 런타임에 유효한 상대 URL을 생성 하는 방법을 제공 하는 것입니다.

## <a name="usingandresolveclienturl"></a>Using`~`and`ResolveClientUrl`

대신 절대 URL를 하드 코딩 보다 ASP.NET을 사용 하면 페이지 개발자가 물결표를 사용 하도록 (`~`) 웹 응용 프로그램의 루트를 나타냅니다. 예를 들어, 표기법 사용이 자습서의 앞부분에 나오는 `~/Admin/Default.aspx` 참조 텍스트에는 `Default.aspx` 페이지에 `Admin` 폴더. 합니다 `~` 나타냅니다는 `Admin` 폴더가 웹 응용 프로그램의 루트의 하위 폴더입니다.

합니다 `Control` 클래스의 [ `ResolveClientUrl` 메서드](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) URL을 사용 하 고 컨트롤이 상주 하는 웹 페이지에 대 한 적절 한 상대 URL을 수정 합니다. 예를 들어, 호출 `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` 에서 `About.aspx` 반환 `Images/PoweredByASPNET.gif`합니다. 하지만 호출한 `~/Admin/Default.aspx`를 반환 `../Images/PoweredByASPNET.gif`합니다.

> [!NOTE]
> 모든 ASP.NET 서버 컨트롤에서 파생 되므로 합니다 `Control` 클래스를 모든 서버 컨트롤에 액세스할 수는 `ResolveClientUrl` 메서드. 도 `Page` 클래스에서 파생 되는 `Control` 클래스, 즉 ASP.NET 페이지의 코드 숨김 클래스에서 직접이 메서드를 사용할 수 있습니다.


### <a name="usingin-the-declarative-markup"></a>사용 하 여`~`선언적 태그에

URL 관련 속성을 포함 하는 여러 ASP.NET 웹 컨트롤로: 하이퍼링크 컨트롤에는 `NavigateUrl` 속성, 컨트롤에 이미지를 `ImageUrl` 속성 등에입니다. 이러한 컨트롤에 해당 URL 관련 속성 값을 전달할를 렌더링할 때 `ResolveClientUrl`합니다. 따라서 이러한 속성을 포함 하는 경우는 `~` 웹 응용 프로그램의 루트를 가리키는 URL 유효한 상대 URL로 수정 됩니다.

ASP.NET 서버 컨트롤에만 변환 하는 염두에 둡니다는 `~` 해당 URL 관련 속성에서입니다. 경우는 `~` 와 같은 정적 HTML 태그에 표시 됩니다 `<img src="~/Images/PoweredByASPNET.gif" />`, ASP.NET 엔진은 전송는 `~` 나머지 HTML 콘텐츠와 함께 브라우저로 합니다. 브라우저에 있다고 가정 합니다 `~` URL의 일부입니다. 예를 들어 태그를 수신 하는 브라우저 `<img src="~/Images/PoweredByASPNET.gif" />` 라는 하위 폴더는 가정 `~` 하위 폴더를 사용 하 여 `Images` 이미지 파일이 포함 된 `PoweredByASPNET.gif`합니다.

이미지 태그를 해결 하려면 `Site.master`, 기존 대체 `<img>` ASP.NET 이미지 웹 컨트롤을 사용 하 여 요소입니다. 이미지 웹 컨트롤의 설정 `ID` 하 `PoweredByImage`, 해당 `ImageUrl` 속성을 `~/Images/PoweredByASPNET.gif`, 및 해당 `AlternateText` "ASP.NET에서 전원!" 속성


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

이 변경의 마스터 페이지에 확인 한 후 다시 방문는 `~/Admin/Default.aspx` 페이지를 다시 합니다. 이 이번에는 `PoweredByASPNET.gif` 이미지 파일 페이지에 나타납니다 (그림 3 참조). 이미지 웹 컨트롤을 렌더링할 때이 사용 합니다 `ResolveClientUrl` 해결 방법 해당 `ImageUrl` 속성 값입니다. `~/Admin/Default.aspx` 는 `ImageUrl` 을 적절 한 상대 URL의 HTML 소스 다음 코드 조각으로 변환 됩니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> URL 기반 웹 컨트롤 속성에 사용 될 뿐만 아니라 합니다 `~` 호출 하는 경우에 사용할 수는 `Response.Redirect` 및 `Server.MapPath` 특히 메서드. 또한 합니다 `ResolveClientUrl` 필요한 경우 ASP.NET 또는 마스터 페이지의 선언적 태그에서 직접 메서드를 호출할 수 있습니다를 참조 하세요 [Fritz Onion](https://www.pluralsight.com/blogs/fritz/)의 블로그 항목 [사용 하 여 `ResolveClientUrl` 태그에서](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)합니다.


## <a name="fixing-the-master-pages-remaining-relative-urls"></a>마스터 페이지의 상대 Url을 나머지 수정

외에 `<img>` 요소에는 `footerContent` 방금 고정을 마스터 페이지는 주의 기울여야 하는 하나 이상의 상대 URL이 포함 합니다. 합니다 `topContent` "마스터 페이지 자습서"를 가리키는 링크를 포함 하는 지역 `Default.aspx`합니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

사용자가이 URL을 상대 하기 때문에 전송할는 `Default.aspx` 콘텐츠 페이지를 방문 하는 것의 폴더에는 페이지입니다. 항상이 링크를 `Default.aspx` 바꾸려면 먼저 루트 폴더에는 `<a>` 하이퍼링크 웹을 사용 하 여 요소를 사용할 수 있도록 제어는 `~` 표기법.

제거는 `<a>` 요소 태그 및 해당 위치에 하이퍼링크 컨트롤을 추가 합니다. 하이퍼링크의 설정 `ID` 하 `lnkHome`, 해당 `NavigateUrl` 속성을 `~/Default.aspx`, 및 해당 `Text` 속성을 "마스터 페이지 자습서입니다."


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

정말 간단하죠. 이 시점에 마스터 페이지 및 콘텐츠 페이지를 폴더에 관계 없이 콘텐츠 페이지에 의해 렌더링 되는 경우에 제대로 Url 마스터 페이지에 기반한 모든이 있습니다.

### <a name="automatic-url-resolution-in-theheadsection"></a>자동 URL 해상도`<head>`섹션

에 [ *사이트 전체 레이아웃을 사용 하 여 마스터 페이지 만들기* ](creating-a-site-wide-layout-using-master-pages-cs.md) 추가한 자습서를 `<link>` 에 `Styles.css` 파일는 `<head>` 지역:


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

동안 합니다 `<link>` 요소의 `href` 특성은 상대, 런타임 시 적절 한 경로 자동으로 변환 됩니다. 설명한 대로 합니다 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서는 `<head>` 지역은 실제로 서버 쪽 컨트롤을 수정할 수 있습니다는 렌더링 될 때 해당 내부 컨트롤의 내용입니다.

이 확인 하려면 다시는 `~/Admin/Default.aspx` 페이지 및 브라우저에 보내지는 HTML 소스를 보고 합니다. 아래 코드 조각에서 볼 수 있듯이 합니다 `<link>` 요소의 `href` 특성을 적절 한 상대 URL을 자동으로 수정 된 `../Styles.css`합니다.


[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>요약

마스터 페이지 링크, 이미지 및 URL을 통해 지정 해야 하는 다른 외부 리소스에 자주 포함 됩니다. 마스터 페이지 및 콘텐츠 페이지를 같은 폴더에 존재 하지 않을 이므로 abstain 상대 Url을 사용 해야 합니다. 하드 코드 된 절대 Url을 사용할 수 있지만, 웹 응용 프로그램 절대 URL을 결합 하므로 긴밀 하 게 수행 합니다. 절대 URL 변경 처럼 자주 이동 또는 웹 응용 프로그램-배포-돌아가서 절대 Url을 업데이트 해야 해야 합니다.

물결표를 사용 하는 이상적인 방법입니다 (`~`) 응용 프로그램 루트를 나타냅니다. URL 관련 속성을 포함 하는 ASP.NET 웹 컨트롤로 매핑하는 `~` 런타임 시 응용 프로그램 루트에. 웹 컨트롤 사용 하 여 내부적으로 `Control` 클래스의 `ResolveClientUrl` 유효한 상대 URL을 생성 하는 방법입니다. 이 메서드는 공용 및 모든 서버 컨트롤에서 사용할 수 있습니다 (포함 하는 `Page` 클래스) 이므로 사용할 수 있습니다 프로그래밍 방식으로 코드 숨김 클래스에서 필요한 경우.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET의 마스터 페이지](http://www.odetocode.com/Articles/419.aspx)
- [마스터 페이지에서 기준 주소 다시 지정 URL](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [사용 하 여 `ResolveClientUrl` 태그](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [다음](control-id-naming-in-content-pages-cs.md)
