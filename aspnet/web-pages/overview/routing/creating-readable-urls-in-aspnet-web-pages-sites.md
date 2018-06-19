---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 읽을 수 있는 Url을 만들면 | Microsoft Docs
author: tfitzmac
description: 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트 및 어떻게 이렇게 하면 더 쉽게 읽고 SEO에 더 나은 있는 Url을 사용 하 여의 라우팅 설명 합니다. 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 7858b7cbd6dccafb2867ed9a1d102561e211e435
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529752"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트 및 어떻게 이렇게 하면 더 쉽게 읽고 SEO에 더 나은 있는 Url을 사용 하 여의 라우팅 설명 합니다.
> 
> 학습 내용:
> 
> - ASP.NET 사용 하는 방법 라우팅 보다 읽기 쉽고 검색 가능한 Url을 사용할 수 있도록 합니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="about-routing"></a>라우팅에 대 한

사이트의 페이지에 대 한 Url 얼마나 잘 사이트 작동에 영향을 줄 수 있습니다. URL을 &quot;친숙 한&quot; 사이트를 사용 하기 쉽게 만들 수 있습니다. 사이트에 대 한 검색 엔진 최적화 (SEO)와 함께 유용할 수 있습니다. ASP.NET 웹 사이트는 친화적 Url을 자동으로 사용 하는 기능을 포함 합니다.

ASP.NET에는 방금 서버에서 파일을 가리키는 대신 사용자 조치에 설명 하는 의미 있는 Url을 만들 수 있습니다. 이러한 Url에 대해 고려할 가상의 블로그:

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

다음 항목에 해당 Url을 비교 합니다.

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

첫 번째 쌍에서 사용자 알고 있어야 합니다 블로그를 사용 하 여 표시 되는 *blog.cshtml* 페이지와 오른쪽 범주 또는 날짜 범위를 가져오는 쿼리 문자열을 구성 해야 합니다. 두 번째 예제 집합 이해 하 고 만드는 훨씬 쉽습니다.

또한 첫 번째 예에 대 한 Url을 특정 파일에 직접 가리키도록 (*blog.cshtml*). 어떤 이유로 블로그 이동 된 경우 다른 폴더를 서버에서 나 블로그 다른 페이지를 사용 하도록 다시 작성 된 경우 링크는 잘못 된 것입니다. Url의 두 번째 집합은 특정 페이지를 가리키지 않습니다. 하더라도 블로그 구현 또는 위치 변경, Url은의 결과가 계속 유효 합니다.

ASP.NET 웹 페이지에서 ASP.NET을 사용 하기 때문에 위의 예제에서와 같이 친숙 한 Url을 만들 수 있습니다 *라우팅*합니다. 라우팅 요청을 수행할 수 있는 페이지 (또는 페이지)에 URL에서 논리적 매핑을 만듭니다. 매핑이 논리 이므로 (하지 물리적, 특정 파일에), 라우팅은 다양 한 사이트에 대 한 Url을 정의 하는 방법을 제공 합니다.

## <a name="how-routing-works"></a>라우팅의 작동 원리

ASP.NET 요청을 처리할 때 URL을 전달 하는 방법을 결정 읽습니다. ASP.NET 때 개별 세그먼트에 대 한 URL 디스크의 파일에서 왼쪽에서 오른쪽으로 이동 합니다. 일치 하는 경우 페이지를 전달 되는 URL에 남아 있는 모든 항목 *경로 정보*합니다.

다른 사용자가이 URL을 사용 하 여 요청을 가정해 봅니다.

`http://www.contoso.com/a/b/c`

검색을 다음과 같이 진행합니다.

1. 파일의 이름 및 경로 거기 */a/b/c.cshtml*? 이 경우 해당 페이지를 실행 하 고 없는 정보를 전달 합니다. 그렇지 않은 경우...
2. 파일의 이름 및 경로 거기 */a/b.cshtml*? 따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `c` 를 합니다. 그렇지 않은 경우...
3. 파일의 이름 및 경로 거기 */a.cshtml*? 따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `b/c` 를 합니다.

더 정확 하 게 찾을 수 검색에 대 한 일치 하는 경우 *.cshtml* 가 지정 된 폴더의 파일, ASP.NET 계속 이러한 파일에 대 한 차례로 찾습니다.

1. */a/b/c/default.cshtml* (경로 정보 없음).
2. */a/b/c/index.cshtml* (경로 정보 없음).

> [!NOTE]
> 분명히, 특정 페이지에 대 한 요청 (즉, 포함 된 요청이 *.cshtml* 파일 이름 확장명) 예상 하는 것 처럼 작동 합니다. 요청을 같은 `http://www.contoso.com/a/b.cshtml` 페이지를 실행 *b.cshtml* 제대로 합니다.


페이지, 내부 페이지의를 통해 경로 정보를 얻을 수 `UrlData` 속성이 사전 설정 되어 만들어져야 합니다. 라는 파일이 있다고 가정해 보세요. *ViewCustomers.cshtml* 사이트가이 요청을 가져옵니다.

`http://mysite.com/myWebSite/ViewCustomers/1000`

위 규칙에 표시 된 것과 같이 페이지 요청이 전달 됩니다. 다음 페이지를 가져와 경로 정보를 표시 하는 다음과 같은 코드를 사용할 수 있습니다 (이 경우 값 &quot;1000&quot;):

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 라우팅 전체 파일 이름을 포함 하지 않습니다, 때문에 있을 수 있습니다 모호성으로 인해 동일한 페이지가 있는 경우 이름 하지만 서로 다른 파일 이름 확장명 (예를 들어 *MyPage.cshtml* 및 *MyPage.html*) . 라우팅을 사용 하 여 문제를 방지 하기 위해서는 없는지 페이지 이름이 해당 확장만 다른 사이트에 있는지 확인 하는 것이 좋습니다.


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[WebMatrix-Url, UrlData 및 SEO에 대 한 라우팅](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)합니다. Mike Brind 하 여이 블로그 항목 라우팅의 작동 원리 ASP.NET 웹 페이지에 대 한 추가 정보를 제공합니다.
