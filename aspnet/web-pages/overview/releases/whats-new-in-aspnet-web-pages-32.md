---
uid: web-pages/overview/releases/whats-new-in-aspnet-web-pages-32
title: 3.2 페이지 Asp.net의 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 06/30/2014
ms.assetid: a652beff-8e6b-48ad-bfe4-3703f7ccf0a5
msc.legacyurl: /web-pages/overview/releases/whats-new-in-aspnet-web-pages-32
msc.type: authoredcontent
ms.openlocfilehash: a55c01c1430b983fbe34654cc2c00de05e941d71
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802253"
---
<a name="whats-new-in-aspnet-web-pages-32"></a>ASP.NET Web Pages 3.2의에서 새로운 기능
====================
[Microsoft](https://github.com/microsoft)

이 항목에서는 웹 페이지 3.2.2 ASP.NET Web Pages 3.2의 새로운 기능을 설명 하 고 [웹 페이지 3.2.3 beta1](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)

## <a name="aspnet-web-pages-32"></a>ASP.NET Web Pages 3.2

이 릴리스에 버그를 수정 하 고 새로운 기능 중 하나를 소개 합니다.

## <a name="download"></a>다운로드

NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다. 모든 런타임 패키지를 수행 합니다 [유의 적 버전](http://semver.org/) 사양입니다. ASP.NET 웹 페이지 3.2 패키지에 버전: &ldquo;3.2.0&rdquo;합니다. 설치 하거나 이러한 패키지를 통해 업데이트할 수 있습니다 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebPages/)합니다. 릴리스에 NuGet의 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](whats-new-in-aspnet-web-pages-32/samples/sample1.cmd)]

## <a name="new-feature-and-bug-fix"></a>새로운 기능 및 버그 수정

한 버그를 수정 하 고이 릴리스에서 사소한 기능 개선 사항 중 하나를 수행 합니다. 동일한 쿼리를 찾을 수 있습니다 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC|v5.2%20RTM&amp;assignedTo=All&amp;component=Web%20Pages%2FRazor&amp;sortField=Id&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)합니다.

## <a name="aspnet-web-pages-322"></a>ASP.NET Web Pages 3.2.2

이 릴리스에서 롤백합니다 접속 변경는 [ASP.NET Web Pages 3.2.1 베타 릴리스 버전](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) 큰 razor 페이지 렌더링 성능이 크게 향상을 제공 하는 합니다. 참조[Codeplex 문제 585](https://aspnetwebstack.codeplex.com/workitem/585)합니다. 이 릴리스에서 MVC 5.2.2 부합 패키지는 이제이 버전에 따라 다릅니다.

큰 페이지 렌더링 MSN 팀과 협력 합니다. 페이지 80kb가 넘는 데이터를 렌더링 하는 경우 얻게 대형 개체 힙의 개체입니다. 레이아웃의 여러 계층을 사용 하는 경우이 효과 곱한 수 있습니다.

서버에서 결과 추가 CPU 사용량, 메모리 및 한참 더 긴 보존 하는 동안 일시 중지 [Gen 2 정리](https://msdn.microsoft.com/en-us/library/ms973837.aspx) 가비지 수집기에서 합니다.

다음은 분석 결과 보여 주는 테이블을 [perfview](https://channel9.msdn.com/Series/PerfView-Tutorial) 실행 합니다. 큰 페이지를 렌더링 하는 동안 CPU 약 68% 상수 유지 됩니다. 테이블 2 세대 수집 횟수 거의 완전히 제거 하 고 결과 더 높은 요청 속도 및 가비지 수집으로 인해 일시 중지에 상당한 감소를 보여 줍니다.

| **영역** | **(3.2) before** | **(3.2.1) 후** | **델타 %** |
| --- | --- | --- | --- |
| 총 요청 (개수) | 26,986 | 32,591 | <font style="background-color: #4bacc6">20.80%</font> |
| 추적 기간 (초) | 196.20 | 198.60 | 1.20% |
| 요청/초 | 137.53 | 164.10 | <font style="background-color: #4bacc6">19.30%</font> |
| CPU 부하 | 68.80% | 68.50% |  -0.40% |
| GC CPU 샘플 | 124,323 | 17,543 | <font style="background-color: #4bacc6">-85.90%</font> |
| 총 할당 (개수) | 55,357,146 | 57,222,949 | 3.40% |
| 총 GC 일시 중지 (샘플) | 15,091 | 8,515 | <font style="background-color: #4bacc6">-43.60%</font> |
| Gen0 GC (개수) | 403 | 1,216 | 201.70% |
| Gen1 GC (개수) | 290 | 367 | 26.60% |
| Gen2 GC (개수) | 229 | 2 | <font style="background-color: #00ff00">-99.10%</font> |
| CPU / (샘플/요청) 요청 | 19.73 | 16.47 | -16.50% |

| 색 구분: | <font style="background-color: #00ff00">Core 개선</font> | <font style="background-color: #4bacc6">성능에 긍정적인 영향</font> |
|---------------|-----------------------------------------------------------------|-------------------------------------------------------------------------------|
|               |                                                                 |                                                                               |

## <a name="aspnet-web-pages-323-beta1"></a>ASP.NET 웹 페이지 3.2.3 beta1

이 릴리스에 버그 수정만 포함 됩니다. 사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20Pages%2FRazor&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 해결 된 문제 목록을 확인 합니다.
