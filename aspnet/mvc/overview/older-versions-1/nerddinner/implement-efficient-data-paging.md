---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: "효율적인 데이터 페이징을 구현 | Microsoft Docs"
author: microsoft
description: "8 단계에는 한 번에 dinners의 단위: 1000s를 표시 하는 대신 것만 표시에 예정 된 dinners 10 있도록 페이징 지원을 우리의 /Dinners URL을 추가 하는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 0b0fba604f97d3bb72d2d403e643b422b9ce48bd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="implement-efficient-data-paging"></a>효율적인 데이터 페이징을 구현합니다
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 8 단계로 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 8 단계에는 한 번에 dinners의 단위: 1000s를 표시 하는 대신 것만 표시 10 예정 된 dinners-한 번에 되 고 최종 사용자가 전체 목록을 SEO 친화적인 방식에서 앞뒤로 이동 하며 다시 페이지 수 있도록 우리의 /Dinners URL에 대 한 페이징 지원을 추가 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-8-paging-support"></a>업그레이드 되었으며 수정 8 단계: 페이징 지원

사이트에 성공한 경우 예정 된 dinners 수천을 갖습니다. UI 조정 이러한 dinners 모두 처리 하 고 사용자가 찾아볼 수 있도록 해야 합니다. 이 작업이 가능 하려면 페이징 지원을 추가 합니다 우리의 */Dinners* dinners의 1000s에서는 한 번에 표시 하는의 대신 URL 합니다만-한 번에 10 예정 된 dinners 표시 및 최종 사용자가 전체 목록에서 앞뒤로 이동 하며 백 페이지 수 SEO 친숙 한 방법입니다.

### <a name="index-action-method-recap"></a>Index () 동작 방법 간략하게 설명

Index () 동작 메서드가 DinnersController 클래스 내에서 현재과 같은 형식 아래:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

요청 하면는 */Dinners* URL을 모든 향후 dinners의 목록을 검색 하 고 모든 여 목록이 렌더링 합니다.

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a>이해 IQuerable&lt;T&gt;

*IQueryable&lt;T&gt;*  LINQ 사용 하 여.NET 3.5의 일부로 도입 된 인터페이스입니다. 에서는 사용할 수 있는의 페이징 지원을 구현 하는 강력한 "지연 된 실행" 시나리오를 사용 합니다.

우리의 DinnerRepository에서 우리 반환 하는 경우 IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 시퀀스:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 반환 된 개체는 LINQ to SQL 사용 하 여 데이터베이스에서 Dinner 개체를 검색 하는 쿼리를 캡슐화 합니다. 중요 한 사실은 tolist () 메서드를 호출 하거나 액세스/는 쿼리의 데이터를에서 반복 하려고 하면 될 때까지 데이터베이스에 대해 쿼리를 실행 되지 않습니다. 우리의 FindUpcomingDinners() 메서드를 호출 하는 코드는 IQueryable에 "연결 된" 작업/필터를 추가 하도록 선택할 수도&lt;Dinner&gt; 쿼리를 실행 하기 전에 개체입니다. LINQ to SQL은 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하지 못합니다.

페이징 논리를 구현 하려면 업데이트 하면 다음과 같이 우리의 DinnersController index () 동작 메서드에 추가 "Skip"과 "사용" 연산자는 반환 된 IQueryable에 적용 되도록&lt;Dinner&gt; 시퀀스에 tolist () 호출 하기 전에:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

위의 코드는 데이터베이스에 있는 처음 10 개의 예정 된 dinners 다루지 않으며 하 고 20 dinners 다시 돌아갑니다. LINQ to SQL은 SQL 데이터베이스-와 웹 서버에 없는 논리를 건너뛰는 중 수행 하는 최적화 된 SQL 쿼리를 생성 합니다. 즉, 예정 된 Dinners 수많은 데이터베이스에 있는, 경우에 원하는 10만 (있어 효율적이 고 확장 가능한)이 요청의 일부로 검색 됩니다.

### <a name="adding-a-page-value-to-the-url"></a>URL에 "페이지" 값 추가

대신를 하드 코딩 하는 특정 페이지 범위는 사용자가 요청 하는 Dinner 범위를 나타내는 "페이지" 매개 변수를 포함 하도록 Url 바랍니다.

#### <a name="using-a-querystring-value"></a>쿼리 문자열 값을 사용 하 여

아래의 코드 우리의 index () 동작 메서드를 쿼리 문자열 매개 변수를 지원 하 고 같은 Url을 사용 하려면 업데이트 하면 어떻게 설명 */Dinners? 페이지 2 =*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

위의 index () 동작 메서드 매개 변수 이름 "페이지"에 있습니다. 매개 변수는 null을 허용 정수로 선언 (즉 어떤 int? 나타냅니다). 즉는 */Dinners? 페이지 2 =* URL 값이 "2" 매개 변수 값으로 전달 하도록 발생 합니다. */Dinners* (querystring 값)이 없는 URL에는 null 값이 전달 될 발생 합니다.

페이지 크기 (이 경우 10 행)에 따라 페이지 값을 곱하여 우리를 건너 뛰 개수 dinners 확인 하려면 됩니다. 사용 하 여 ["C# null 병합" 연산자 (?) ](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) nullable 형식을 처리할 때 유용 합니다. 위의 코드 페이지 매개 변수가 null 이면 페이지 0의 값을 할당 합니다.

#### <a name="using-embedded-url-values"></a>포함 된 URL 값을 사용 하 여

쿼리 문자열 값을 사용 하는 대신 실제 URL 자체 내에서 페이지 매개 변수를 포함할 수 있습니다. 예를 들어: */Dinners/Page/2* 또는 */Dinners/2*합니다. ASP.NET MVC에는 다음과 같은 시나리오를 지원 하기 위해 활용할 수 있는 강력한 URL 라우팅 엔진 포함 되어 있습니다.

수신 하는 URL 또는 URL 형식을 원하는 모든 컨트롤러 클래스 또는 동작 메서드에 매핑되는 사용자 지정 라우팅 규칙을 등록할 수 있습니다. 이 프로젝트 내에서 Global.asax 파일을 여는 해야 할 일:

![](implement-efficient-data-paging/_static/image2.png)

다음 경로에 첫 번째 호출 처럼 MapRoute() 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 하십시오. 아래 MapRoute():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

위에 "UpcomingDinners" 이라는 새 라우팅 규칙을 등록 하는 것입니다. URL 형식은 있음을 나타냅니다 합니다. "Dinners/페이지 / {페이지}" – 여기서 {페이지}은 URL 내에 포함 된 매개 변수 값입니다. MapRoute() 메서드를 세 번째 매개 변수는이 형식을 DinnersController 클래스에 index () 동작 메서드에 일치 하는 Url을 매핑할 해야 있습니다를 나타냅니다.

해야 하기 전에 쿼리 문자열-이 시나리오와 URL과 쿼리 문자열 하지에서 가져온 우리의 "페이지" 매개 변수는 이제 점을 제외 하 고 정확한 동일한 index () 코드를 사용할 수 있습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

이제 응용 프로그램을 실행 하 고를 입력 했습니다 및 */Dinners* 처음 10 개의 예정 된 dinners 보겠습니다.

![](implement-efficient-data-paging/_static/image3.png)

여기서 입력 하 고 */Dinners/Page/1* dinners의 다음 페이지를 살펴보겠습니다.

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>페이지 탐색 UI 추가

페이징 시나리오를 완료 하기 위한 마지막 단계는 사용자가을 쉽게 Dinner 데이터에 대해 건너뛸 수 있도록 우리의 보기 템플릿 내에서 "다음" 및 "이전" 탐색 UI를 구현 하 됩니다.

이 올바르게 구현 하려면 해야 데이터베이스에 Dinners의 총 수를 아는 데이터의 여러 페이지를 변환 하는 방식입니다. 그런 다음는 데이터의 끝 부분이 나 부분에 현재 요청 된 "페이지" 값이 있는지 여부를 계산 하 고 표시 하거나 그에 따라 "이전" 및 "다음" UI를 숨길 수 해야 합니다. 구현 하 여이 논리는 index () 작업 메서드 내에서. 또는 더 재사용 가능한 방식으로이 논리를 캡슐화 하는 프로젝트에는 도우미 클래스를 추가할 수 있습니다.

다음 목록에서 파생 되는 간단한 "PaginatedList" 도우미 클래스를은&lt;T&gt; 에 기본 제공 컬렉션 클래스는.NET Framework입니다. IQueryable 데이터의 모든 연속 페이지를 매기는 데 사용할 수 있는 재사용 가능한 컬렉션 클래스를 구현 합니다. 이 업그레이드 되었으며 수정 응용 프로그램에서 되 겠 IQueryable을 통해 작동&lt;Dinner&gt; 하지만 결과 쉽게 사용 될 수 IQueryable&lt;제품&gt; 또는 IQueryable&lt;고객&gt;다른 응용 프로그램 시나리오에서 발생 합니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

위의 계산 방법 및 다음 속성을 노출 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"와 같은 있습니다. 그 후 컬렉션에 있는 데이터 페이지의 시작 이나는 원래 시퀀스의 끝이를 나타내는 두 개의 도우미 속성 "HasPreviousPage" 및 "HasNextPage"를 표시 합니다. 위의 코드에서는 두 개의 SQL 쿼리 Dinner 개체의 총 수를 검색할 때 첫 번째 실행-수를 발생 시킵니다 (이 개체를 반환 하지 않는 – 대신 정수를 반환 하는 "SELECT COUNT" 문을 수행)의 행만 검색 하 고 두 번째 데이터의 현재 페이지에 대 한 데이터베이스에서 필요한 데이터입니다.

PaginatedList 만들려는 DinnersController.Index() 도우미 메서드를 업데이트할 수 있습니다&lt;Dinner&gt; 우리의 DinnerRepository.FindUpcomingDinners()에서 결과, 우리의 템플릿 보기에 게 전달 합니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

ViewPage 상속할 \Views\Dinners\Index.aspx 뷰 템플릿을 업데이트할 수 있습니다&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt; ViewPage 대신&lt;IEnumerable&lt;Dinner&gt;&gt;을 표시 하거나 숨기려면 다음 및 이전 탐색 UI 우리의 보기 템플릿 맨 아래에 다음 코드를 추가 합니다.

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

위의 Html.RouteLink() 도우미 메서드를 사용 하는 하이퍼링크를 생성할 우리는 방법을 확인 합니다. 이 메서드는 이전에 사용한 Html.ActionLink() 도우미 메서드는 비슷합니다. 쿼리하여 Global.asax 파일 내에서 설정 하는 규칙을 라우팅 "UpcomingDinners"를 사용 하 여 URL을 생성 하기는 다릅니다. 이렇게 하면 형식 취급 index () 동작 메서드에 Url을 생성 합니다 म: */Dinners/페이지 / {페이지}* – 여기서 {페이지} 값은 변수를 제공 하 고 위에 현재 PageIndex 기반 합니다.

지금 응용 프로그램을 실행할 때 다시 보게 한 번에 10 dinners 브라우저에:

![](implement-efficient-data-paging/_static/image5.png)

이 밖에도 &lt; &lt; &lt; 및 &gt; &gt; &gt; 탐색 UI 통해 전달 건너뛰고 이전 버전과 사용 하 여이 데이터를 통해 엔진 액세스할 수 있는 Url을 검색 하는 페이지의 맨 아래에:

![](implement-efficient-data-paging/_static/image6.png)

| **쪽 주제: IQueryable의 의미를 이해 하&lt;T&gt;** |
| --- |
| IQueryable&lt;T&gt; 는 다양 한 흥미로운 지연 된 실행 시나리오를 사용 하도록 설정 하는 매우 강력한 기능 (페이징 및 컴퍼지션와 마찬가지로 쿼리 기반). 으로 모든 강력한 기능이 사용법에 주의를 기울여야을 남용 되지 있는지 확인 합니다. 해당 반환 IQueryable 인식 해야&lt;T&gt; 리포지토리에서 결과 호출 코드에 연결 된 연산자 메서드를 추가 하 고 최고의 쿼리 실행에 참여 하므로를 사용 하도록 설정 합니다. 호출 코드에이 기능을 제공 하지 않을 경우 되돌려야 IList 다시&lt;T&gt; 또는 IEnumerable&lt;T&gt; 가 이미 실행 된 쿼리의 결과 포함 하는 결과-합니다. 페이지 매김 시나리오에 대 한 해야 실제 데이터 페이지 매김 논리 호출 되는 저장소 메서드에 푸시 수 있습니다. 이 시나리오에서는 우리의 FindUpcomingDinners() finder 메서드를 사용 하려면 한 PaginatedList를 반환 하거나 서명 업데이트 될 수 있습니다: PaginatedList&lt; Dinner&gt; FindUpcomingDinners (pageIndex int, int pageSize) {} 반환 IList 또는 &lt;Dinner&gt;, param 아웃 "totalCount"를 사용 하 여 Dinners의 총 수를 반환 하: IList&lt;Dinner&gt; FindUpcomingDinners (pageIndex int, int totalCount out int pageSize) {} |

### <a name="next-step"></a>다음 단계

이제 살펴보겠습니다 응용 프로그램에 인증 및 권한 부여 지원을 추가할 수 있는 방법.

>[!div class="step-by-step"]
[이전](re-use-ui-using-master-pages-and-partials.md)
[다음](secure-applications-using-authentication-and-authorization.md)
