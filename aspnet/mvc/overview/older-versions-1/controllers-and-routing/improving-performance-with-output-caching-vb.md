---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 캐싱 (VB)를 출력으로 성능 향상 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법에 대해 알아봅니다. 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: debc456531ee771a9ecb24b81e35d3084d8e49b8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398361"
---
<a name="improving-performance-with-output-caching-vb"></a>출력 캐싱 (VB)를 사용 하 여 성능 향상
====================
[Microsoft](https://github.com/microsoft)

> 이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법에 대해 알아봅니다. 동일한 콘텐츠를 각 시간 작업을 호출 하는 새 사용자를 만들 필요가 없습니다 있도록 컨트롤러 작업에서 반환 된 결과 캐시 하는 방법을 알아봅니다.


이 자습서의 목표는 출력 캐시를 활용 하 여 ASP.NET MVC 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법을 설명 합니다. 출력 캐시를 사용 하면 컨트롤러 작업에 의해 반환 된 콘텐츠를 캐시할 수 있습니다. 이런 방식으로 동일한 콘텐츠를 매번 동일한 컨트롤러 작업이 호출 됩니다 생성할 필요가 없습니다.

예를 들어, ASP.NET MVC 응용 프로그램 데이터베이스 레코드의 목록을 Index 라는 보기에 표시 되는지 한다고 가정 합니다. 일반적으로 각 시간 인덱스 뷰를 반환 하는 컨트롤러 작업을 호출 하는 사용자는 데이터베이스 레코드 집합을 검색 해야 데이터베이스에서 데이터베이스 쿼리를 실행 하 여 합니다.

출력 캐시를 활용을 사용 하는 반면, 하는 경우 다음 방지할 수 있습니다 누구나 동일한 컨트롤러 작업을 호출 될 때마다 데이터베이스 쿼리를 실행. 뷰는 컨트롤러 작업에서 다시 생성 하는 대신 캐시에서 검색할 수 있습니다. 서버에서 작동 하면 캐싱 수행 중복을 방지할 수 있습니다.

#### <a name="enabling-output-caching"></a>출력 캐싱을 사용 하도록 설정

추가 하 여 출력 캐싱을 사용 하도록 설정 하는 &lt;OutputCache&gt; 개별 컨트롤러 작업 또는 전체 컨트롤러 클래스는 특성입니다. 예를 들어 목록 1에서 컨트롤러 index () 라는 작업을 노출 합니다. Index () 작업의 출력은 10 초 동안 캐시 됩니다.

**1 – Controllers\HomeController.vb 나열**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


ASP.NET MVC의 베타 버전에서는 출력 캐싱에 적합 하지 않습니다과 같은 URL [ http://www.MySite.com/ ](http://www.mysite.com/)합니다. 과 같은 URL을 입력 해야 하는 대신 [ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)합니다.


목록 1의 index () 작업의 출력은 10 초 동안 캐시 됩니다. 원하는 경우 훨씬 더 캐시 기간을 지정할 수 있습니다. 예를 들어, 하루에 대 한 컨트롤러 작업의 출력을 캐시 하려는 경우 다음 지정할 수 있습니다 캐시 기간 86400 초 (60 초 \* 60 분 \* 24).

콘텐츠가 보장할 수 없습니다 지정 된 시간 동안 캐시 됩니다. 메모리 리소스가 부족 해질, 캐시 제거 콘텐츠가 자동으로 시작 합니다.

목록 1에서 Home 컨트롤러 목록 2에서 인덱스 뷰를 반환합니다. 이 보기에 대 한 특별 합니다. 인덱스 보기는 현재 시간을 표시 하기만 하면 됩니다 (그림 1 참조).

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**그림 1-캐시 된 인덱스 뷰**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

브라우저의 주소 표시줄에 URL /Home/인덱스를 입력 하 고 반복적으로 다음 인덱스 뷰에서 표시 되는 시간과 브라우저에서 새로 고침/다시 로드 단추에 도달 하 여 index () 작업을 여러 번 호출 하는 경우 10 초 동안 변경 되지 않습니다. 보기 캐시 되므로 한 번 표시 됩니다.

동일한 뷰 응용 프로그램을 방문 하는 모든 사람에 대 한 캐시 되는 이해 하는 것이 반드시 합니다. Index () 작업을 호출 하는 모든 사람이 동일한 캐시 된 버전을 인덱스 뷰의 받습니다. 즉, 웹 서버, 인덱스 뷰를 제공 하기 위해 수행 해야 하는 작업의 크기는 크게 줄어듭니다.

매우 간단한 할 일 목록 2 뷰 발생 합니다. 현재 뷰를 표시합니다. 그러나 캐시 된 데이터베이스 레코드 집합을 표시 하는 보기 쉽게 처럼 수 있습니다. 이 경우 데이터베이스 레코드 집합은 각 시간 보기를 반환 하는 컨트롤러 동작을 호출 하는 데이터베이스에서 검색할 수 필요가 없습니다. 캐싱은 웹 서버와 데이터베이스 서버에서 수행 해야 하는 작업의 양을 줄일 수 있습니다.

페이지를 사용 하지 마세요 &lt;% @ OutputCache %&gt; MVC 뷰의 지시문입니다. 이 지시문은 Web Forms를 통해 bleeding는 ASP.NET MVC 응용 프로그램에서는 사용할 수 없습니다. 

#### <a name="where-content-is-cached"></a>콘텐츠가 캐시 된

기본적으로 사용 하는 경우는 &lt;OutputCache&gt; 특성, 콘텐츠 세 위치에 캐시 된: 웹 서버, 모든 프록시 서버 및 웹 브라우저입니다. 콘텐츠의 Location 속성을 수정 하 여 캐시 된 위치에 정확 하 게 제어할 수 있습니다.는 &lt;OutputCache&gt; 특성입니다.

다음 값 중 하나로 Location 속성을 설정할 수 있습니다.

> · 모든
> 
> · 클라이언트
> 
> · 다운스트림
> 
> · 서버
> 
> · 없음
> 
> · ServerAndClient


기본적으로 위치 속성을 모든 값을 갖습니다. 그러나는 하려는 브라우저 또는 서버에만 캐시 하는 경우가 있습니다. 예를 들어, 각 사용자에 대 한 개인 설정 되는 정보를 캐시 하는 경우 다음 하면 안됩니다 서버의 정보입니다. 다른 사용자에 게 다양 한 정보를 표시 하는 경우 클라이언트에만 정보를 캐시 해야 있습니다.

예를 들어 목록 3에서 컨트롤러를 현재 사용자 이름을 반환 하는 GetName() 라는 작업을 노출 합니다. Jack 웹 사이트에 로그인 하 고 GetName() 작업을 호출 하는 경우 다음 동작 문자열을 반환 합니다 "Hi Jack"입니다. Jill (질) 웹 사이트에 로그인 하 고 GetName() 작업 호출 이후에 다음 그녀는 또한 받습니다 문자열을 "Hi Jack". 문자열은 Jack 컨트롤러 작업을 처음 호출 후 모든 사용자에 대 한 웹 서버에 캐시 됩니다.

**3 – Controllers\BadUserController.vb 나열**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

대부분의 경우 목록 3의 컨트롤러는 원하는 방식으로 작동 하지 않습니다. Jill에 게 "Hi Jack" 메시지를 표시 하지 않으려는 합니다.

서버 캐시에 콘텐츠를 캐시 하지 않아야 합니다. 그러나 다음 성능 향상을 위해 브라우저 캐시에 개인 설정 된 콘텐츠를 캐시 하는 것이 좋습니다. 브라우저에서 콘텐츠를 캐시 하 고 사용자가 여러 번 동일한 컨트롤러 작업을 호출 하는 경우 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.

목록 4의 수정 된 컨트롤러 GetName() 작업의 출력을 캐시합니다. 그러나 콘텐츠는 브라우저 및 서버에 없는 캐시 됩니다. 이런 방식으로 여러 사용자가 GetName() 메서드를 호출 하는 경우, 각 사용자는 자신의 사용자 이름 및 다른 사람의 사용자 이름을 가져옵니다.

**4-Controllers\UserController.vb 나열**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

에 &lt;OutputCache&gt; 4 특성 OutputCacheLocation.Client 값으로 설정 된 위치 속성을 포함 합니다. 합니다 &lt;OutputCache&gt; 특성 NoStore 속성에도 포함 되어 있습니다. NoStore 속성은 캐시 된 콘텐츠를의 영구 복사본을 저장 하지 마십시오 프록시 서버와 브라우저 알리는 데 사용 됩니다.

#### <a name="varying-the-output-cache"></a>출력 캐시를 변경

경우에 따라 다른 캐시 된 버전의 동일한 콘텐츠 좋습니다. 예를 들어 마스터/세부 정보 페이지를 만든다고 가정해 보겠습니다. 마스터 페이지에는 영화 제목 목록을 표시합니다. 제목을 클릭 하면 선택한 동영상에 대 한 세부 정보를 가져옵니다.

세부 정보 페이지 캐시 하면, 동일한 동영상에 대 한 세부 정보 클릭 하면 어떤 영화에 관계 없이 표시 됩니다. 첫 번째 사용자가 선택한 첫 번째 영화의 모든 이후 사용자에 게 표시 됩니다.

VaryByParam 속성 활용 하 여이 문제를 해결할 수는 &lt;OutputCache&gt; 특성입니다. 이 속성을 사용 하면 서로 다른 캐시 된 버전 때 폼 매개 변수와 동일한 콘텐츠를 만들 수 있습니다 또는 쿼리 문자열 매개 변수 달라 집니다.

예를 들어 목록 5의 컨트롤러 Master() 및 Details() 라는 두 가지 작업을 노출 합니다. Master() 작업 영화 타이틀의 목록을 반환 하 고 Details() 작업 선택한 동영상에 대 한 세부 정보를 반환 합니다.

**5-Controllers\MoviesController.vb 나열**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Master() 동작 값을 사용 하 여 VaryByParam 속성을 포함 "none"입니다. 작업을 호출할 Master() 동일한 캐시 된 버전의 마스터를 볼 때 반환 됩니다. 매개 변수는 모든 형식 매개 변수 또는 쿼리 문자열 무시 (그림 2 참조).

**그림 2 – /Movies/Master 보기**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**그림 3 – / Movies/세부 정보 보기**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Details() 작업에는 "Id" 값을 사용 하 여 VaryByParam 속성을 포함 합니다. Id 매개 변수에 다른 값 컨트롤러 작업에 전달 하는 경우 다른 캐시 된 버전의 세부 정보 보기 생성 됩니다.

것이 줄이고 이상의 캐싱 VaryByParam 속성 결과 사용 하는 이해 해야 합니다. 자세히 보기의 다른 캐시 된 버전의 Id 매개 변수에 각 버전에 대해 만들어집니다.

VaryByParam 속성은 다음 값으로 설정할 수 있습니다.

> \* = 폼 또는 쿼리 문자열 매개 변수 다릅니다 때마다 다른 캐시 된 버전을 만듭니다.
> 
> none = 사용 안 함 다양 한 캐시 된 버전을 만들려면
> 
> 매개 변수 목록을 세미콜론으로 폼 또는 쿼리 문자열 매개 변수 목록의 다릅니다 때마다 다른 캐시 된 버전을 만들기 =


#### <a name="creating-a-cache-profile"></a>캐시 프로필 만들기

속성을 수정 하 여 출력 캐시 속성을 구성 하는 대신 합니다 &lt;OutputCache&gt; 특성인 웹 구성 (web.config) 파일에서 캐시 프로필을 만들 수 있습니다. 웹 구성 파일에서 캐시 프로필을 만드는 몇 가지 중요 한 이점 제공 합니다.

첫째, 웹 구성 파일에서 출력 캐시를 구성 하 여 컨트롤러 작업에서 하나의 중앙 위치에서 콘텐츠를 캐시 하는 방법을 제어할 수 있습니다. 캐시 프로필을 두 개 만들고 여러 컨트롤러 또는 컨트롤러 작업 프로필을 적용할 수 있습니다.

둘째, 응용 프로그램을 다시 컴파일하지 않고 웹 구성 파일을 수정할 수 있습니다. 프로덕션 환경에 이미 배포 된 응용 프로그램에 대 한 캐싱을 사용 하지 않도록 설정 해야 할 경우 다음 수정할 수 있습니다 단순히 웹 구성 파일에 정의 된 캐시 프로필. 웹 구성 파일에 변경 내용을 자동으로 검색 되어 적용 됩니다.

예를 들어 합니다 &lt;캐싱&gt; Cache1Hour 명명 된 캐시 프로필을 정의 하는 웹 구성 섹션 6 나열 합니다. 합니다 &lt;캐싱&gt; 섹션 내에 나타나야 합니다 합니다 &lt;system.web&gt; 웹 구성 파일의 섹션입니다.

**코드 6 – web.config에 대 한 캐싱 섹션**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

7의 컨트롤러 Cache1Hour 프로필을 사용 하 여 컨트롤러 작업에 적용 하는 방법을 보여 줍니다.는 &lt;OutputCache&gt; 특성입니다.

**Listing 7 – Controllers\ProfileController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

7의 컨트롤러에 의해 노출 index () 작업을 호출 하는 경우 동시는 1 시간 동안 반환 됩니다.

#### <a name="summary"></a>요약

출력 캐싱을 크게 ASP.NET MVC 응용 프로그램의 성능을 향상 시키기 위해 쉽게 메서드를 사용 하 여 제공 합니다. 이 자습서에서는 사용 하는 방법을 배웠습니다 합니다 &lt;OutputCache&gt; 특성을 컨트롤러 작업의 출력을 캐시 합니다. 또한 속성을 수정 하는 방법을 배웠습니다 합니다 &lt;OutputCache&gt; 콘텐츠가 캐시 되는 방식을 수정 하려면 기간과 VaryByParam 속성과 같은 특성입니다. 마지막으로 웹 구성 파일에서 캐시 프로필을 정의 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [이전](understanding-action-filters-vb.md)
> [다음](adding-dynamic-content-to-a-cached-page-vb.md)
