---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징 구현 | Microsoft Docs
author: microsoft
description: 8 단계 대신 dinners 한 번에 수천 개의 표시만 표시 됩니다에서 10 향후 dinners 있도록 /Dinners URL 페이징 지원을 추가 하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2bef690355cd1f89a15a67f0c49775296d551136
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837531"
---
<a name="implement-efficient-data-paging"></a>효율적인 데이터 페이징 구현
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 8 단계로 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 8 단계 dinners 한 번에 수천 개의 표시 하는 대신 수만 번-10 향후 dinners 표시 하 고 다시 페이지를 앞뒤로 전체 목록 SEO 친숙 한 방식으로 최종 사용자를 허용 /Dinners URL에 대 한 페이징 지원을 추가 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-8-paging-support"></a>NerdDinner 8 단계: 페이징 지원

사이트에 성공한 경우 향후 dinners 수천 해야 합니다. UI 모두 이러한 dinners 처리 크기를 조정 하 고 찾아볼 수 있도록 허용 하는지 확인 해야 합니다. 이 작업이 가능 하도록 페이징 지원을 추가한 우리의 */Dinners* 에서는 한 번에 수천 개의 dinners 표시의 URL에서는 표시 10 향후 dinners-번 하 고 최종 사용자의 전체 목록을 통해 앞뒤로 페이지 뒤로 허용 SEO 친숙 한 방법입니다.

### <a name="index-action-method-recap"></a>Index () 작업 메서드 요약

Index () 작업 메서드에서 DinnersController 클래스 내에서 현재 같습니다 아래:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

요청 하면를 */Dinners* URL 모든 향후 dinners 목록을 검색 하 고 모든 수의 목록을 렌더링 합니다.

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a>이해 IQuerable&lt;T&gt;

*IQueryable&lt;T&gt;*  LINQ를 사용 하 여.NET 3.5의 일부로 도입 하는 인터페이스입니다. 에서는 사용할 수 있는의 페이징 지원을 구현 하기 위해 강력한 "지연 된 실행" 시나리오를 사용 합니다.

우리의 DinnerRepository에서 IQueryable 받았다고 했습니다&lt;Dinner&gt; FindUpcomingDinners() 메서드 시퀀스:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 반환 된 개체를 LINQ to SQL 사용 하 여 데이터베이스에서 Dinner 개체를 검색할 쿼리를 캡슐화 합니다. 중요 한 점은 tolist () 메서드를 호출 하거나 쿼리에서 데이터에 대해 액세스/반복 시도 될 때까지 데이터베이스에 대해 쿼리를 실행 하지 않습니다 것입니다. FindUpcomingDinners() 메서드를 호출 하는 코드를 IQueryable "연결된" 작업/필터를 추가 하도록 선택할 수도&lt;Dinner&gt; 쿼리를 실행 하기 전에 개체입니다. LINQ to SQL은 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하지 못합니다.

페이징 논리를 구현 하려면 업데이트할 수 있습니다 추가 "Skip" 및 "Take" 연산자는 반환 된 IQueryable에 적용 되도록이 DinnersController index () 작업 메서드&lt;Dinner&gt; tolist ()를 호출 하기 전에 시퀀스:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

위의 코드는 데이터베이스의 처음 10 개 향후 dinners 건너뜁니다 및 다시 20 dinners 반환 합니다. LINQ to SQL은 웹 서버 및 SQL database –의 논리를 건너뛰는 중 수행 하는 최적화 된 SQL 쿼리를 생성 합니다. 즉, 한 예정 된 Dinners 수백만 개의 데이터베이스의 경우에 원하는 10만 (있으므로 효율적이 고 확장 가능한)이 요청의 일부로 검색 됩니다.

### <a name="adding-a-page-value-to-the-url"></a>URL에 "페이지" 값을 추가합니다.

하드 코딩 대신 특정 페이지 범위에는 사용자가 요청 하는 Dinner 범위를 나타내는 "페이지" 매개 변수를 포함 하도록 Url 하 려 합니다.

#### <a name="using-a-querystring-value"></a>쿼리 문자열 값을 사용 하 여

아래 코드 쿼리 문자열 매개 변수를 지원 하 고 같은 Url을 사용 하도록 설정 하는 우리의 index () 작업 메서드를 업데이트 하는 방법을 보여 줍니다 */Dinners? 페이지 2 =*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

위의 index () 작업 메서드는 "페이지" 라는 매개 변수. Nullable 정수로 선언 된 매개 변수 (어떤 int는? 나타냅니다). 즉 합니다 */Dinners? 페이지 = 2* URL 값이 "2" 매개 변수 값으로 전달할 발생 합니다. 합니다 */Dinners* URL (쿼리 문자열 값)이 없는 null 값이 전달 하면 됩니다.

건너뛸 수 dinners 결정할 페이지 크기 (이 경우 10 행)에 따라 페이지 값을 곱하여 됩니다 했습니다. 사용 하 여 [C# null "병합" 연산자 (?) ](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) nullable 형식을 처리할 때 유용 합니다. 위의 코드 페이지 매개 변수가 null 이면 페이지 값이 0 할당 합니다.

#### <a name="using-embedded-url-values"></a>포함 된 URL 값을 사용 하 여

쿼리 문자열 값을 사용 하는 대신 실제 URL 자체 내에서 페이지 매개 변수를 포함 하는 것입니다. 예를 들어: */Dinners/Page/2* 하거나 *Dinners/2*합니다. ASP.NET MVC에는 이와 같은 시나리오를 지원 하기 위해 활용할 수 있는 강력한 URL 라우팅 엔진을 포함 합니다.

모든 들어오는 URL 또는 URL 형식을 원하는 모든 컨트롤러 클래스 또는 동작 메서드에 매핑되는 사용자 지정 라우팅 규칙을 등록할 수 있습니다. 할 일 됩니다 프로젝트 내에서 Global.asax 파일을 엽니다.

![](implement-efficient-data-paging/_static/image2.png)

및 다음 첫 번째 경로 같은 MapRoute() 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 합니다. MapRoute() 아래:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

위의 "UpcomingDinners" 이라는 새 라우팅 규칙을 등록 하는 것입니다. URL 형식은 나타내는 됩니다 것 "Dinners/페이지 / {페이지}" – {page} 인 URL 내에 포함 된 매개 변수 값입니다. MapRoute() 메서드에 세 번째 매개 변수 DinnersController 클래스에 index () 작업 메서드에이 형식과 일치 하는 Url 매핑하는 것을 나타냅니다.

앞에서 사용한 Querystring 시나리오-를 사용 하 여 URL과 쿼리 문자열 하지에서 가져온이 "페이지" 매개 변수는 이제 점을 제외 하 고 정확 하 게 동일한 index () 코드를 사용할 수 했습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

이제 응용 프로그램을 실행 하 고 입력 했습니다 */Dinners* 처음 10 개 향후 dinners를 살펴보겠습니다.

![](implement-efficient-data-paging/_static/image3.png)

에서는 입력 */Dinners/Page/1* dinners의 다음 페이지를 살펴보겠습니다.

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>페이지 탐색 UI를 추가합니다.

페이징 시나리오를 완료 하기 위한 마지막 단계 Dinner 데이터를 쉽게 건너뛸 수 있도록 하려면 우리의 보기 템플릿에서 "다음" 및 "이전" 탐색 UI를 구현 해야 합니다.

이 올바르게 구현 하기에서는 알아야 Dinners 총 데이터베이스에도로 변환 됩니다이 데이터 페이지 수는 방법입니다. 그런 다음 시작 또는 데이터의 끝에서 현재 요청 된 "페이지" 값이 있는지 여부를 계산 및 표시 하거나 숨기기 "이전" 및 "다음" UI를 적절 하 게 해야 합니다. index () 작업 메서드 내에서이 논리를 구현할 수 것입니다. 또는 더 재사용 가능한 방식으로이 논리를 캡슐화 하는 프로젝트에는 도우미 클래스를 추가할 수 했습니다.

목록에서 파생 되는 간단한 "PaginatedList" 도우미 클래스는 다음과 같습니다&lt;T&gt; 에 기본 제공 컬렉션 클래스는.NET Framework입니다. 페이지를 매기 IQueryable 데이터의 모든 시퀀스는 다시 사용할 수 있는 컬렉션 클래스를 구현 합니다. NerdDinner 응용 프로그램에서 마련 IQueryable을 통해 작동&lt;Dinner&gt; 하지만 결과 쉽게 사용 될 수 IQueryable&lt;제품&gt; 또는 IQueryable&lt;고객&gt;다른 응용 프로그램 시나리오에서 발생 합니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

계산 하는 방법을 위의 예제와 다음 속성을 노출 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"입니다. 또한 다음 컬렉션에 있는 데이터 페이지의 시작 또는 원래 시퀀스의 끝에 있는지 여부를 나타내는 두 개의 도우미 속성 "HasPreviousPage" 및 "HasNextPage"를 표시 합니다. 위의 코드는 두 SQL 쿼리 실행 수 Dinner 개체의 총 수를 검색할 첫 번째를 하면 (이 개체를 반환 하지 않습니다 – 대신 정수를 반환 하는 "SELECT COUNT" 문을 수행) 및 두 번째의 행만 검색 현재 페이지 데이터에 대 한 데이터베이스에서 필요한 데이터입니다.

DinnersController.Index() 도우미 메서드는 PaginatedList를 만들려면 다음 업데이트할 수 있습니다&lt;Dinner&gt; 우리의 DinnerRepository.FindUpcomingDinners()에서 결과 보기 템플릿은로 전달 하 합니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

그런 다음 ViewPage 상속할 \Views\Dinners\Index.aspx 보기 템플릿을 업데이트할 수 있습니다&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt; ViewPage 대신&lt;IEnumerable&lt;Dinner&gt;&gt;를 표시 하거나 숨기려면 다음 및 이전 탐색 UI 보기-템플릿의 맨 아래에 다음 코드를 추가 합니다.

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

어떻게 Html.RouteLink() 도우미 메서드를 사용 하 여는 하이퍼링크를 생성은에서는 위의 알 수 있습니다. 이 메서드는 이전에 사용한 Html.ActionLink() 도우미 메서드는 비슷합니다. 차이점 "UpcomingDinners" 라우팅 Global.asax 파일 내에서 설정 하는 규칙을 사용 하 여 URL을 생성 하는 것입니다. 형식이 index () 동작 메서드에 Url 생성 하는 것이 이렇게: */Dinners/페이지 / {page}* – {page} 값이 제공 하 고 위에서 현재 PageIndex 기반 변수 위치입니다.

고 이제 응용 프로그램 실행 하면 다시 한 번에 10 dinners 브라우저에서:

![](implement-efficient-data-paging/_static/image5.png)

이 밖에도 &lt; &lt; &lt; 하 고 &gt; &gt; &gt; 탐색 전달 건너뛰고 이전 버전과 사용 하 여 데이터를 통해 엔진 액세스할 수 있는 Url을 검색할 수 있는 페이지의 맨 아래에 UI:

![](implement-efficient-data-paging/_static/image6.png)

| **쪽 항목: IQueryable의 의미를 이해 하&lt;T&gt;** |
| --- |
| IQueryable&lt;T&gt; 다양 한 흥미로운 지연 된 실행 시나리오를 사용 하도록 설정 하는 매우 강력한 기능입니다 (페이징 및 컴퍼지션과 같은 쿼리 기반). 으로 모든 강력한 기능을 사용 하 여 사용 방법에 주의를 기울여야을 남용 되지 있는지 확인 합니다. 해당 반환 IQueryable을 인식 해야&lt;T&gt; 리포지토리의 결과 호출 코드에 연결 된 연산자 메서드에 추가 하 고 따라서 ultimate 쿼리 실행에 참여를 사용 하도록 설정 합니다. 호출 코드가이 기능을 제공 하지 않을 경우 반환 해야 다시 IList&lt;T&gt; 또는 IEnumerable&lt;T&gt; 이미 실행 하는 쿼리 결과 포함 하는 결과입니다. 페이지 매김 시나리오의 실제 데이터 페이지 매김 논리 호출 되는 리포지토리 메서드로 푸시 해야 함. 이 시나리오에서는 FindUpcomingDinners() finder 메서드 시그니처에서 PaginatedList를 반환 하거나 업데이트 될 수 있습니다: PaginatedList&lt; Dinner&gt; FindUpcomingDinners (pageIndex int, int pageSize) {} 반환 IList 또는 &lt;Dinner&gt;, "totalCount" out 매개 변수를 사용 하 여 Dinners의 총 개수를 반환 합니다: IList&lt;Dinner&gt; FindUpcomingDinners (pageIndex int, int totalCount 아웃 int pageSize) {} |

### <a name="next-step"></a>다음 단계

이제 살펴보겠습니다 응용 프로그램에 대 한 인증 및 권한 부여 지원을 추가할 수 있습니다 하는 방법.

> [!div class="step-by-step"]
> [이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)
