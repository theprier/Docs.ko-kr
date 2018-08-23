---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 페이지 (Razor) 사이트를 Asp.net에서 읽을 수 있는 Url 만들기 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 웹 사이트를 ASP.NET Web Pages (Razor) 및 읽을 수 있는 및 SEO에 대 한 향상 된 Url을 선택할 수 있습니다 하는 방법의 라우팅 설명 합니다. 하겠습니다...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: b8405283dc5bf44a4cd8d1122d327346774d95e8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831579"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 웹 사이트를 ASP.NET Web Pages (Razor) 및 읽을 수 있는 및 SEO에 대 한 향상 된 Url을 선택할 수 있습니다 하는 방법의 라우팅 설명 합니다.
> 
> 학습할 내용:
> 
> - 어떻게 ASP.NET 라우팅을 사용 하 여 더 읽기 쉽고 검색 가능한 Url을 사용할 수 있도록 합니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="about-routing"></a>라우팅 정보

사이트의 페이지에 대 한 Url에 얼마나 잘 사이트 작동에 영향 있을 수 있습니다. URL 이지요 &quot;친숙 한&quot; 사이트를 사용 하는 데 쉽게 수 있습니다. 또한 사이트에 대 한 검색 엔진 최적화 (SEO)를 사용 하 여는 것이 도움이 됩니다. ASP.NET 웹 사이트 Url을 자동으로 사용 하는 기능을 포함 합니다.

ASP.NET을 통해 방금 서버에서 파일을 가리키는 대신 사용자 작업을 설명 하는 의미 있는 Url을 만들 수 있습니다. 이러한 Url에 대해 고려할 가상의 블로그:

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

다음에 해당 Url을 비교 합니다.

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

블로그를 사용 하 여 표시 되는 알고 첫 번째 쌍은 사용자가 해야 합니다 *blog.cshtml* 페이지 및 올바른 범주 또는 날짜 범위를 가져오는 쿼리 문자열을 구성 해야 합니다. 두 번째 예제 집합을 만들어 이해할 훨씬 쉽습니다.

첫 번째 예제에 대 한 Url도 직접 가리키도록 특정 파일 (*blog.cshtml*). 어떤 이유로 블로그 된 다른 폴더로 이동할 서버의 또는 블로그 다른 페이지를 사용 하도록 다시 작성 된 경우 링크는 잘못 된 것입니다. Url의 두 번째 집합을 특정 페이지를 가리키지 않습니다.도 블로그 구현 또는 위치를 변경 하는 경우, Url은 계속 유효 합니다.

ASP.NET Web Pages에서 ASP.NET을 사용 하기 때문에 위의 예제에서와 같이 친숙 한 Url을 만들 수 있습니다 *라우팅*합니다. 라우팅 요청을 수행할 수 있는 URL 페이지 (또는 페이지)에서 논리 매핑을 만듭니다. 매핑이 논리 기 때문에 사이트에 대 한 Url을 정의 하는 방법에 뛰어난 유연성을 제공 라우팅 (물리적이 지 특정 파일을)를 합니다.

## <a name="how-routing-works"></a>라우팅의 작동 원리

ASP.NET 요청을 처리할 때 URL이 라우팅하는 방법을 결정을 읽습니다. ASP.NET는 왼쪽에서 오른쪽으로 이동 하는 디스크, 파일에 URL의 개별 세그먼트를 일치 시 키 려 합니다. 일치 하는 경우 페이지에 전달 됩니다 URL에 남아 있는 모든 항목 *경로 정보*합니다.

이 URL을 사용 하 여 요청을 수행 하는 사용자가 있다고 가정해 봅시다.

`http://www.contoso.com/a/b/c`

검색은 다음과 같이 이루어집니다.

1. 파일의 이름과 경로 사용 하 여 거기 */a/b/c.cshtml*? 그렇다면 해당 페이지를 실행 하 고 전달할 정보가 없습니다. 그렇지 않은 경우...
2. 파일의 이름과 경로 사용 하 여 거기 */a/b.cshtml*? 따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `c` 되도록 합니다. 그렇지 않은 경우...
3. 파일의 이름과 경로 사용 하 여 거기 */a.cshtml*? 따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `b/c` 되도록 합니다.

더 정확 하 게 찾을 수 검색에 대 한 일치 하는 경우 *.cshtml* 가 지정 된 폴더의 파일을 ASP.NET 계속 해 서 이러한 파일에:

1. */a/b/c/default.cshtml* (경로 정보 없음).
2. */a/b/c/index.cshtml* (경로 정보 없음).

> [!NOTE]
> 그렇다고 해 특정 페이지에 대 한 요청 (즉, 포함 하는 요청은 *.cshtml* 파일 이름 확장명) 예상한 것 처럼 작동 합니다. 와 같은 요청 `http://www.contoso.com/a/b.cshtml` 페이지에 실행될지 *b.cshtml* 아무 문제 없이 합니다.


페이지 내에서 페이지를 통해 경로 정보를 얻을 수 있습니다 `UrlData` 속성 사전입니다. 라는 파일에 있다고 가정해 보십시오 *ViewCustomers.cshtml* 사이트가이 요청을 가져옵니다.

`http://mysite.com/myWebSite/ViewCustomers/1000`

위의 규칙에서 설명한 대로, 요청 페이지로 이동 됩니다. 페이지 내에서 가져오고 경로 정보를 표시 하려면 다음과 같은 코드를 사용할 수 있습니다 (이 경우 값 &quot;1000&quot;):

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 라우팅 전체 파일 이름을 포함 하지 않습니다, 때문에 있을 수 있습니다 모호성은 동일 페이지가 있는 경우 다른 파일 이름 확장명 (예를 들어 *MyPage.cshtml* 하 고 *MyPage.html*) . 라우팅을 사용 하 여 문제를 방지 하기 위해 없는지 페이지 이름이 해당 확장만 다른 사이트에 있는지 확인 하는 것이 좋습니다.


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[WebMatrix-Url, UrlData 및 SEO에 대 한 라우팅](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)합니다. 이 블로그 항목 Mike Brind 하 여 라우팅 작동 방법을 ASP.NET 웹 페이지에서에 몇몇 추가 세부 정보를 제공합니다.
