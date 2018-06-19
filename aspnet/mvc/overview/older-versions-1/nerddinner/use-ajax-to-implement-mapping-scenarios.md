---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX를 사용 하 여 매핑 시나리오를 구현할 | Microsoft Docs
author: microsoft
description: 11 단계 AJAX 매핑 지원 만들기, 편집 또는 보기 dinners l 볼 수 있는 사용자를 사용 하면이 업그레이드 되었으며 수정 응용 프로그램에 통합 하는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 4b3f1e46886c4c1f054e43768b0a44695d71bf09
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872717"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX를 사용 하 여 매핑 시나리오를 구현 하려면
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 11 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 11 단계 AJAX 매핑을 지원 하므로 만들기, 편집 또는 보기 dinners dinner의 위치를 그래픽으로 볼 수 있는 사용자가 업그레이드 되었으며 수정 응용 프로그램에 통합 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>업그레이드 되었으며 수정 11 단계: AJAX 지도 통합

이제 약간 시각적으로 멋진 AJAX 매핑 지원 통합 하 여 응용 프로그램을 만들 것 것입니다. 이렇게 하면 사용자가 만들기, 편집 또는 보기 dinners dinner의 위치를 그래픽으로 볼 수 있습니다.

### <a name="creating-a-map-partial-view"></a>지도 부분 뷰 만들기

응용 프로그램 내의 여러 위치에서 매핑 기능을 사용 하도록 하겠습니다. 여러 컨트롤러 작업 및 보기에서 다시 사용할 수 있는 단일 부분 템플릿 내에서 일반적인 지도 기능을 캡슐화 하에서는 드라이 코드를 유지 합니다. 이 부분 뷰 "map.ascx" 이름을 알아보고 \Views\Dinners 디렉터리 내에서 만들 하겠습니다.

만들 수 있습니다는 map.ascx 부분 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가 기능 선택 하 여&gt;보기 메뉴 명령입니다. "Map.ascx" 뷰의 이름을 부분 뷰로 확인 하 고 강력한 형식의 "Dinner" 모델 클래스를 전달 하려고는 나타내는 합니다 했습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

"추가" 단추를 클릭 하는 경우이 부분 템플릿 생성 됩니다. 다음 Map.ascx 파일에 다음 내용을 업데이트 합니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

첫 번째 &lt;스크립트&gt; Microsoft 가상 지구 6.2 매핑 라이브러리 알려야 합니다. 두 번째 &lt;스크립트&gt; 트 공통 Javascript 매핑 논리를 캡슐화 할는 곧 만들 map.js 파일에 요소를 참조 합니다. &lt;div id = "theMap"&gt; 요소는 Virtual Earth 하는 지도 호스트 하는 데 사용할 HTML 컨테이너입니다.

그런 다음 포함 된 있는 &lt;스크립트&gt; 이 보기에만 두 JavaScript 함수가 포함 된 블록입니다. 첫 번째 함수 jQuery를 사용 하 여 유선 전화 접속 페이지는 클라이언트 쪽 스크립트를 실행할 준비가 될 때 실행 하는 함수입니다. LoadMap() 도우미 함수를 호출 하기 가상 표면 맵 컨트롤을 로드할 쿼리하여 Map.js 스크립트 파일 내에서 정의 하겠습니다. 두 번째 함수는 위치를 식별 하는 지도에 pin을 추가 하는 콜백 이벤트 처리기.

서버 쪽 사용 방법을 확인 &lt;% = %&gt; 위도 및 경도 JavaScript에 매핑하려고 하기 Dinner 포함 하려면 클라이언트 쪽 스크립트 블록 내에서 블록입니다. 이것이 (호출 하지 않아도 별도 AJAX 서버에 다시 – 값을 검색 하므로 더 빠르게) 클라이언트 쪽 스크립트에서 사용할 수 있는 동적 값을 출력 하는 유용한 방법입니다. &lt;% = %&gt; 보기-서버에서 렌더링 하는 때 블록을 실행할 아니며 하므로 html 출력은 방금 결국 포함 된 JavaScript 값 (예: var 위도 = 47.64312;).

### <a name="creating-a-mapjs-utility-library"></a>Map.js 유틸리티 라이브러리 만들기

이제이 맵에 대 한 JavaScript 기능을 캡슐화 (및 위의 LoadMap 및 LoadPin 메서드 구현)에 사용할 수 있는 Map.js 파일을 만들어 보겠습니다. 우리의 프로젝트 내에서 \Scripts 디렉터리를 마우스 오른쪽 단추로 클릭 하 여이 작업을 수행 하 고 다음 선택할 수 있습니다는 "추가-&gt;새 항목" 메뉴 명령을 JScript 항목 선택 하 고 "Map.js" 라는 이름을 지정 합니다.

다음은 JavaScript 코드를 추가할 것이 지도 표시 하 우리의 dinners에 대 한 위치 핀을 추가 하려면 Virtual Earth와 상호 작용 하는 Map.js 파일에:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>만들기 및 편집 양식와 지도 통합

이제 기존 만들기 및 편집 시나리오와 지도 지원을 통합 합니다 했습니다. 다행히도 있다는이 쉽게 할 일 않아도 컨트롤러 코드 중 하나를 변경 합니다. 우리의 만들기 및 편집 뷰 dinner 폼 UI를 구현 하는 일반적인 "DinnerForm" 부분 뷰를 공유 하므로 한 곳에서 지도 추가 하 고 두 당사의 만들기 및 편집 시나리오를 사용 하 여 수 했습니다.

해야 할 일은 \Views\Dinners\DinnerForm.ascx 부분 뷰를 열고 우리의 새 맵을 부분을 포함 하도록 업데이트 합니다. 업데이트 된 DinnerForm 모양은 지도 추가 되 면 같습니다 (참고: HTML 폼 요소는 코드를 코드 조각에서 생략):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

위의 부분 DinnerForm (때문에 Dinner 개체 뿐만 아니라 국가의 dropdownlist를 채우는 데 SelectList) 해당 모델 유형에 변수로 "DinnerFormViewModel" 형식의 개체를 사용 합니다. 부분 우리의 지도 하기만 "Dinner" 형식의 개체 모델 형식은, 및 하므로 지도 부분 렌더링 म म 전달 하는 Dinner 하위 속성만 DinnerFormViewModel의에:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

JavaScript 함수 "Address" HTML 텍스트 상자에 "흐림 효과" 이벤트를 연결할 부분 사용 하 여 jQuery를 추가 했습니다. 들어보았을 클릭할 때 발생 하는 "포커스" 이벤트 또는 탭의는 상자에 붙여넣습니다. 반대 작업은 사용자를 맞추면 textbox 종료 될 때 발생 하는 "흐림 효과" 이벤트입니다. 이 문제가 발생 되 고 다음 우리의 지도에 새 주소 위치를 표시 하는 경우 위의 이벤트 처리기 위도 및 경도 textbox 값을 지웁니다. Map.js 파일 내에서 정의 하는 콜백 이벤트 처리기 경도 및 위도 입력란을 제공 하는 주소에 따라 가상 표면에서 반환 된 값을 사용 하 여 폼에 업데이트할 됩니다.

고 이제이 응용 프로그램을 다시 실행 하 고 우리의 표준 Dinner 폼 요소와 함께 표시 매핑할 기본 보겠습니다 "호스트 Dinner" 탭을 클릭 했습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

주소를 입력 하 고 번 탭, 위치를 표시 하려면 지도 동적으로 업데이트 됩니다 하며 이벤트 처리기 위도/경도 입력란 위치 값으로 채워집니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

새 dinner를 저장 하 고 편집을 위해 다시 열, 페이지가 로드 될 때 지도 위치가 표시 됩니다 소요 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

주소 필드가 변경 될 때마다 지도 위도/경도 좌표를 업데이트 합니다.

저녁 위치를 표시 하는 지도, 했으므로 표시 텍스트 상자 대신 되므로 숨겨진된 요소 (지도 자동으로 업데이트 하는 주소를 입력 때마다) 없도록 위도 및 경도 양식 필드도 변경할 수 있습니다. 할 일이 Html.Hidden() 도우미 메서드를 사용 하 여 Html.TextBox() HTML 도우미를 사용 하 여 전환:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

및 이제는 폼 좀 더 친숙함 하 고 원시 위도/경도 여전히 데이터베이스에서 각 Dinner로 저장) 하는 것 (동안 표시 되지 않도록 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>자세히 보기와 지도 통합

만들기 및 편집 시나리오와 통합 하는 지도 만들었으므로 이제 해당 보겠습니다도와 통합 세부 정보 시나리오입니다. 호출 하는 것 해야 할 일 &lt;%Html.RenderPartial("map"); %&gt; 자세히 보기 내에서.

다음은 소스 코드를 지도 통합) (사용 하 여 전체 세부 정보 뷰 모양을입니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

고 이제 /Dinners/세부 정보 / [id] URL에는 사용자가 지도에 dinner 위치 저녁에 대 한 세부 정보 표시 됩니다 (압정을 갖춘 때 위로 가져갈 표시 dinner 제목과 그 주소), RSVP fo에 대 한 AJAX 링크가 있고 r 하기:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>데이터베이스 저장소에 위치 검색 구현

AJAX 구현을 완료 하려면 사용자가 그래픽으로 dinners 근처를 검색할 수 있는 응용 프로그램의 홈 페이지에 지도 추가 해 보겠습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Dinners에 대 한 radius 위치 기반 검색을 효율적으로 우리의 데이터베이스 및 데이터 저장소 계층 내에서 지원 구현부터 시작 합니다. 사용 하 여 새 [SQL 2008의 지리 공간 기능](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) ,이 구현 하려면 또는 Gary 드 라이덴 문서 여기에서 설명 하는 SQL 함수 접근 방식을 사용할 수 있습니다 또는: [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 및 Rob Conery 여기에 linq to SQL 사용 하는 방법에 대 한 blogged: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

이 기법을 구현 하려면 됩니다 Visual Studio 내에서 "서버 탐색기" 열, 선택 업그레이드 되었으며 수정 데이터베이스 및 그 아래에서 "기능" 하위 노드에서 마우스 오른쪽 단추로 클릭 하 고 새 "스칼라 반환 함수 만들기"를 선택:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

म 합니다 다음 다음 DistanceBetween 함수에 붙여 넣습니다.

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

다음 만들겠습니다 새 테이블 반환 함수에 SQL Server "NearestDinners" 이라고 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

이 "NearestDinners" 테이블 함수 DistanceBetween 도우미 함수를 사용 하 여 위도의 100 마일 내에서 모든 Dinners를 반환 하 고 제공 म 경도:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

이 함수를 호출 하려면를 먼저 엽니다를 LINQ to SQL 디자이너 우리의 \Models 디렉터리 내 NerdDinner.dbml 파일을 두 번 클릭 하 여:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

그런 다음 SQL 디자이너 우리의 LINQ에서 메서드로 SQL NerdDinnerDataContext 클래스에 추가 하는 LINQ로 NearestDinners 및 DistanceBetween 함수 끌면 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

다음 노출 시킬 수 "FindByLocation" query 메서드 NearestDinner 함수를 사용 하 여 예정 된 반환 하는 DinnerRepository 클래스에 지정된 된 위치의 100 마일 내에 있는 Dinners:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>AJAX JSON 기반 검색 동작 메서드를 구현합니다.

이제 다시 지도 채우는 데 사용할 수 있는 Dinner 데이터의 목록을 반환 하려면 새 FindByLocation() 저장소 메서드를 활용 하는 컨트롤러 동작 메서드에 구현 합니다. 에서는이 동작 메서드에 다시 저녁에에서 데이터를 반환 JSON (JavaScript Object Notation) 형식 쉽게 조작할 수 JavaScript를 사용 하 여 클라이언트에 있도록 해야 합니다.

이 구현 하려면 만들겠습니다 새 "SearchController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가 기능 선택 하 여&gt;컨트롤러 메뉴 명령입니다. 그런 다음 아래와 같은 새 SearchController 클래스 내에서 "SearchByLocation" 작업 메서드 구현:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController의 SearchByLocation 동작 메서드는 내부적으로 DinnerRespository 근처 dinners 목록을 가져오려면에 FindByLocation 메서드를 호출 합니다. 클라이언트에 직접 Dinner 개체를 반환 하지 않고 하지만 그 대신 JsonDinner 개체 반환 합니다. 저녁 속성의 하위 집합을 노출 하는 JsonDinner 클래스 (예: 보안상의 이유로 저녁에 주최 있는 사람의 이름을 공개 하지 않습니다). 저녁 –에 없는 관련 된 특정 dinner RSVP 개체 수를 계산 하 여 동적으로 계산 되는 RSVPCount 속성을 포함 됩니다.

Dinners JSON 기반 통신 형식을 사용 하 여 시퀀스를 반환 하는 컨트롤러의 기본 클래스에서 Json() 도우미 메서드를 사용 다음 했습니다. JSON은 간단한 데이터 구조를 나타내기 위한 표준 텍스트 형식입니다. 다음은 JSON 형식 목록이 두 JsonDinner 개체의 모양을 우리의 동작 메서드에서 반환 되는 경우의 예:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery를 사용 하 여 AJAX JSON 기반 메서드를 호출 합니다.

이제는 SearchController SearchByLocation 동작 메서드를 사용 하도록 업그레이드 되었으며 수정 응용 프로그램의 홈 페이지를 업데이트할 준비가 되었습니다. 할 일이 /Views/Home/Index.aspx 보기 템플릿을 열고 알아보고 textbox, 검색 단추, 우리의 지도 하도록 업데이트 하겠습니다 및 &lt;div&gt; dinnerList 라는 요소:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

다음 페이지에 두 개의 JavaScript 함수를 추가할 수 있습니다.

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

첫 번째 JavaScript 함수 페이지 처음 로드 될 때 지도 로드 합니다. JavaScript 두 번째 JavaScript 함수 와이어 검색 단추 이벤트 처리기를 클릭합니다. 단추가 눌려질 때 우리의 Map.js 파일에 추가 하는 FindDinnersGivenLocation() JavaScript 함수를 호출 합니다.

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

이 FindDinnersGivenLocation() 함수 지도 호출합니다. 가상 지구 컨트롤에 입력 한 중점 find (). Virtual earth 맵 서비스 반환 될 때 지도입니다. Find () 메서드 최종 인수로 전달 म callbackUpdateMapDinners 콜백 메서드를 호출 합니다.

CallbackUpdateMapDinners() 방법은 실제 작업을 수행 하는 위치입니다. – 위도 및 경도 새로 가운데에 맞출지 맵의 전달 우리의 SearchController SearchByLocation() 동작 메서드에 대 한 AJAX 호출을 수행 하려면 jQuery의 $.post() 도우미 메서드를 사용 합니다. $.Post() 도우미 메서드가 완료 되 면 호출 되는 인라인 함수를 정의 하 고 작업 메서드에 전달 됩니다 "dinners" 라는 변수를 사용 하 여 SearchByLocation()에서 JSON 형식 dinner 결과가 반환 됩니다. 각 반환 된 dinner 통해 foreach 않습니다 하 고 dinner의 위도 및 경도 및 기타 속성을 사용 하 여 지도에 새 pin을 추가 합니다. 또한 저녁 항목을 지도의 오른쪽에 dinners HTML 목록에 추가합니다. 그 다음 와이어 접속 압정와 HTML 목록에 마우스 호버 이벤트가 사용자 위로 가져갈 때 dinner에 대 한 세부 정보 표시 되도록:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

및 이제 응용 프로그램을 실행 하 고 우리는 구조와 함께 제공 됩니다 홈 페이지를 방문 했습니다. 도시 이름을 입력 하는 경우 지도 근처 예정 된 dinners 표시 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

마우스로 가리키면는 저녁 항목에 대 한 세부 정보가 표시 됩니다.

저녁 제목을 클릭 나 HTML 목록의 오른쪽에 거품에으로 이동 되 우리 dinner –에 대 한 필요에 따라 RSVP 다음 수 있습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>다음 단계

이제 업그레이드 되었으며 수정 응용 프로그램의 모든 응용 프로그램 기능을 구현 했습니다. 보겠습니다 이제 가능 방법을 살펴보고 자동화 된 단위를 테스트 합니다.

> [!div class="step-by-step"]
> [이전](use-ajax-to-deliver-dynamic-updates.md)
> [다음](enable-automated-unit-testing.md)
