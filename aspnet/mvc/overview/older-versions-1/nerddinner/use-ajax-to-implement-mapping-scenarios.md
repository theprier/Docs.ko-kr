---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX를 사용 하 여 매핑 시나리오 구현 | Microsoft Docs
author: microsoft
description: 11 단계 NerdDinner 응용 프로그램을 작성, 편집 또는 l을 보려는 dinners 보기는 사용자를 사용 하도록 설정 하면 AJAX 매핑 지원을 통합 하는 방법을 표시 하는 중...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f7de23ca46e6dc00fe8075e28068a8b3f95d02cd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823821"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX를 사용 하 여 매핑 시나리오 구현
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 11 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 11 단계 NerdDinner 응용 프로그램을 작성, 편집 또는 dinner의 위치를 그래픽으로 보려면 dinners 보기는 사용자를 사용 하도록 설정 하면 AJAX 매핑 지원을 통합 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner 11 단계: AJAX 지도 통합

이제 약간 시각적으로 흥미로운 AJAX 매핑 지원을 통합 하 여 응용 프로그램을 만들 것 것입니다. 이렇게 하면 만들기, 편집 또는 보기의 저녁 식사 위치를 그래픽으로 보려면 dinners 사용자 활성화 됩니다.

### <a name="creating-a-map-partial-view"></a>지도 부분 뷰 만들기

응용 프로그램 내의 여러 위치에서 매핑 기능을 사용 하려고 합니다. 시험 코드를 유지 하려면 여러 컨트롤러 작업 및 보기에서 다시 사용할 수 있는 단일 부분 템플릿 내에서 공통 맵 기능을 캡슐화 했습니다. "Map.ascx"이 부분 뷰의 이름을 하 고 \Views\Dinners 디렉터리 내에 만들어야 합니다.

만들 수 있습니다는 map.ascx 부분 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;메뉴 명령을 보고 합니다. 에서는 "Map.ascx" 뷰의 이름을, 부분 뷰를 확인 하 고 나타내는 강력한 형식의 "Dinner" 모델 클래스를 전달 하려고 하:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

"추가" 단추를 클릭할 때 부분 템플릿은 생성 됩니다. 다음 내용이 다음 Map.ascx 파일을 업데이트 됩니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

첫 번째 &lt;스크립트&gt; 가리키는 Microsoft Virtual Earth 6.2 매핑 라이브러리를 참조 합니다. 두 번째 &lt;스크립트&gt; 이 일반적인 Javascript 매핑 논리를 캡슐화 할는 곧 만들 map.js 파일을 가리키는 참조 합니다. 합니다 &lt;div id = "theMap"&gt; 요소 Virtual Earth가 지도 호스트 하는 데 사용할 HTML 컨테이너입니다.

그런 다음 포함 된 있습니다 &lt;스크립트&gt; 이 보기에 특정 두 JavaScript 함수를 포함 하는 블록입니다. 첫 번째 함수는 jQuery 유선 전화 접속 페이지가 클라이언트 쪽 스크립트를 실행할 준비가 되 면 실행 되는 함수를 사용 합니다. LoadMap() 도우미 함수를 호출 하기 virtual earth 맵 컨트롤을 로드 하려면 Map.js 스크립트 파일 내에서 정의 됩니다. 두 번째 함수는 위치를 식별 하는 지도에 핀을 추가 하는 콜백 이벤트 처리기입니다.

서버 쪽에서는 사용 하는 방법을 확인할 수 있습니다 &lt;% = %&gt; 위도 및 경도 JavaScript에 매핑할 것임 저녁 식사를 포함 하는 클라이언트 쪽 스크립트 블록 내에서 블록입니다. 이것이 (호출 하지 않아도 별도 AJAX 서버에 다시 – 값을 검색할 수 있도록 빠르게) 클라이언트 쪽 스크립트에서 사용할 수 있는 동적 값을 출력 하는 데 유용한 기술입니다. &lt;% = %&gt; – 서버의 뷰를 렌더링 하는 경우 블록 실행 되 고 따라서 html 출력 방금 결국 포함 된 JavaScript 값을 사용 하 여 (예: var 위도 47.64312; =) 합니다.

### <a name="creating-a-mapjs-utility-library"></a>Map.js 유틸리티 라이브러리 만들기

이 맵에 대 한 JavaScript 기능을 캡슐화 (및 위의 LoadMap 및 LoadPin 메서드 구현)를 사용할 수 있는 Map.js 파일을 이제 만들어 보겠습니다. 수는 프로젝트 내에서 \Scripts 디렉터리를 마우스 오른쪽 단추로 클릭 하 여이 작업을 수행 하 고 선택한를 "추가-&gt;새 항목" 메뉴 명령, JScript 항목을 선택 하 고 "Map.js" 라는 이름을 지정 합니다.

다음 JavaScript 코드를 추가할 것은 지도가 표시는 dinners에 대 한 위치 핀을 추가 하는 Virtual Earth와 상호 작용할 Map.js 파일:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>만들기 및 편집 양식와 지도 통합

이제 기존 만들기 및 편집 시나리오를 사용 하 여 지도 지원을 통합 하겠습니다. 좋은 소식은 손쉽게 할 일은이 및 변경의 컨트롤러 코드를 필요 하지 않습니다. 만들기 및 편집 보기를 사용 하 여 dinner 폼 UI를 구현 하는 일반적인 "DinnerForm" 부분 뷰를 공유 하므로 수 한곳에서 지도 추가 하 고 모두는 만들기 및 편집 시나리오를 사용 하 여.

할 일을 먼저 모든 \Views\Dinners\DinnerForm.ascx 부분 뷰를 열고 새 지도가 부분을 포함 하도록 업데이트 하는 것입니다. 업데이트 된 DinnerForm 모양을 맵에 추가 되 면 다음과 같습니다 (참고: HTML 폼 요소 간략하게 표현 하기 위해 아래 코드 조각에서 생략 됩니다).

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

위의 부분 DinnerForm (Dinner 개체 뿐만 아니라 국가 dropdownlist를 채우는 데 SelectList 하므로) 모델 형식으로 "DinnerFormViewModel" 형식의 개체를 사용 합니다. 부분 지도가 하기만 "Dinner" 형식의 개체 모델 형식은, 및 하므로 지도 부분 렌더링 하는 경우 전달 Dinner 하위 속성만 DinnerFormViewModel의에:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

JavaScript 함수를 "Address" HTML 텍스트 상자에 "흐리게" 이벤트를 연결할 부분에서는 jQuery 추가 했습니다. 텍스트 상자에 이야기를 클릭할 때 발생 하는 "포커스" 이벤트 또는 탭 합니다. 반대는 사용자는 텍스트 상자를 종료 될 때 발생 하는 "흐리게" 이벤트입니다. 위의 이벤트 처리기 문제가 발생 하면이 고 다음이 맵에 새 주소 위치를 그리는 경우 위도 및 경도 텍스트 상자 값을 지웁니다. Map.js 파일 내에 정의한 콜백 이벤트 처리기는 virtual earth 것에 지정 했던 주소를 기반으로 하 여 반환 되는 값을 사용 하 여 폼에 경도 및 위도 텍스트 상자를 업데이트 합니다.

및 이제 다시 응용 프로그램을 실행 하 고는 표준 Dinner 폼 요소와 함께 표시 매핑할 기본값 살펴보겠습니다 "호스트 Dinner" 탭을 클릭 했습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

주소를 입력 하 고 제거를 탭 한 다음, 지도 위치를 표시 하려면 동적으로 업데이트 됩니다 하 고 이벤트 처리기는 위치 값을 사용 하 여 위도/경도 텍스트 상자를 채웁니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

새 저녁 식사를 저장 하 고 편집을 위해 다시 여십시오, 페이지를 로드할 때 지도 위치 표시 되도록 소요 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

주소 필드 변경 될 때마다 맵과 위도/경도 좌표를 업데이트 합니다.

저녁 식사 위치를 표시 하는 지도, 했으므로 대신 숨겨진된 요소가 되도록 (지도 자동으로 업데이트 하는 주소를 입력 하는 각 시간) 이후 표시 텍스트 상자에서 위도 및 경도 양식 필드를 변경할 수도 있습니다. 할 일이 Html.Hidden() 도우미 메서드를 사용 하 여 Html.TextBox() HTML 도우미를 사용 하 여 전환 됩니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

및 이제는 폼은 좀 더 친숙 하 고 원시 위도/경도 (여전히 데이터베이스에서 각 저녁 식사를 사용 하 여 저장) 동안 표시 되지 않도록:

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>세부 정보 보기와 지도 통합

이제는 보겠습니다 만들기 및 편집 시나리오를 사용 하 여 통합 하는 지도 세부 정보 시나리오를 사용 하 여 통합할 수도 있습니다. 모든 할 일을 먼저 호출 하는 것 &lt;Html.RenderPartial("map") %; %&gt; 세부 정보 보기 내에서.

전체 세부 정보 보기 (맵 통합)을 소스 코드의 모양을 다음과 같습니다.

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

이제 사용자가 /Dinners/세부 정보 / [id] URL로 이동할 때 보게 저녁을 지도에 dinner의 위치에 대 한 세부 정보 및 (압정-를 사용 하 여 전체 때 마우스를 가져갈 표시 dinner 제목과의 주소), RSVP fo에 대 한 AJAX 링크가 있고 r 것:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>데이터베이스 및 저장소 위치 검색을 구현합니다.

AJAX 구현은 해제를 완료 하려면 사용자 가까이 dinners 그래픽 방식으로 검색할 수 있도록 응용 프로그램의 홈 페이지에 지도 추가 해 보겠습니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

효율적으로 Dinners radius 위치 기반 검색을 수행 하는 데이터베이스 및 데이터 저장소 계층 내에서 지원 구현부터 시작 합니다. 사용 하 여 새 [SQL 2008의 지리 공간 기능](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 이 구현 하려면 Gary 드 라이덴 문서에서 설명 하는 SQL 함수 방법을 사용할 수 있습니다 또는 또는: [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 한 Rob Conery LINQ to SQL 사용 하 여 여기서 사용 하는 방법에 대 한 블로그 게시물을 올렸습니다. [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

이 기법을 구현 하려면에서는 Visual Studio 내에서 "서버 탐색기", NerdDinner 데이터베이스를 선택 하 고 그 아래에서 "함수" 하위 노드를 마우스 오른쪽 단추로 클릭 열리고 새 "스칼라 반환 함수 만들기"를 선택:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

그런 다음 다음 DistanceBetween 함수에 붙여 넣고:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

그런 다음 새 테이블 반환 함수 "NearestDinners" 이라고 하는 SQL Server에 만듭니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

이 "NearestDinners" 테이블 함수 DistanceBetween 도우미 함수를 사용 하 여 위도의 100 마일 내 모든 Dinners를 반환 하 고 제공 했습니다 경도:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

이 함수를 호출 하려면에서는 먼저 엽니다 LINQ to SQL 디자이너 우리의 \Models 디렉터리 내 NerdDinner.dbml 파일을 두 번 클릭 합니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

에서는에서는 그런 다음 끕니다. NearestDinners 및 DistanceBetween 함수를 LINQ to SQL 디자이너 SQL NerdDinnerDataContext 클래스에는 LINQ의 메서드로 추가 하는:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

예정 된 반환할 NearestDinner 함수를 사용 하는 DinnerRepository 클래스 "FindByLocation" 쿼리 메서드를 노출 합니다에서는 지정 된 위치의 100 마일 내에 있는 Dinners:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON 기반 AJAX 검색 동작 메서드를 구현합니다.

이제 맵을 채우는 데 사용할 수 있는 Dinner 데이터 목록을 다시 반환할 새 FindByLocation() 리포지토리 메서드를 활용 하는 컨트롤러 동작 메서드에 구현 됩니다. 이 동작 메서드에 다시 데이터를 반환할 Dinner JSON (JavaScript Object Notation) 형식으로 쉽게 조작할 수 JavaScript를 사용 하 여 클라이언트에 있도록 해야 합니다.

이 구현 하려면 만들겠습니다 새 "SearchController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;컨트롤러 메뉴 명령입니다. 그런 다음 아래와 같이 새 SearchController 클래스 내에서 "SearchByLocation" 동작 메서드를 구현 하겠습니다.

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

내부적으로 SearchController의 SearchByLocation 작업 메서드는 주변 dinners의 목록을 가져오려면 DinnerRespository에 FindByLocation 메서드를 호출 합니다. 클라이언트에 직접 Dinner 개체를 반환, 보다는 하지만 그 대신 JsonDinner 개체 반환 합니다. 저녁 식사 속성 하위 집합을 노출 하는 JsonDinner 클래스 (예: 보안상의 이유로 저녁 주최 있는 사람의 이름을 공개 하지 않습니다). 또한 Dinner – 존재 하지 않는 한 특정 dinner 연관 RSVP 개체의 수를 계산 하 여 동적으로 계산 되는 RSVPCount 속성을 포함 합니다.

다음 컨트롤러 기본 클래스에서 Json() 도우미 메서드를 사용 하 여 dinners JSON 기반 통신 형식을 사용 하 여 시퀀스를 반환 하는 것입니다. JSON은 간단한 데이터 구조를 나타내기 위한 표준 텍스트 형식입니다. 다음은 두 JsonDinner 개체의 JSON 형식 목록을 모양은 우리의 동작 메서드에서 반환 되는 경우의 예:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>JQuery를 사용 하는 JSON 기반 AJAX 메서드를 호출 합니다.

이제 SearchController의 SearchByLocation 동작 메서드를 사용 하 여 NerdDinner 응용 프로그램의 홈 페이지를 업데이트할 준비가 되었습니다. 할 일이 /Views/Home/Index.aspx 보기 템플릿을 열려면에서는 고 textbox, 검색 단추, 우리의 맵 업데이트와 &lt;div&gt; dinnerList 이라는 요소:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

다음 페이지에 두 개의 JavaScript 함수를 추가할 수 있습니다.

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

페이지가 처음 로드 하는 경우 지도 로드 하는 첫 번째 JavaScript 함수입니다. JavaScript 두 번째 JavaScript 함수 와이어 이벤트 처리기 [검색] 단추를 클릭합니다. 단추를 누르면 Map.js 파일을 추가 하는 FindDinnersGivenLocation() JavaScript 함수를 호출 합니다.

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

이 FindDinnersGivenLocation() 함수 지도 호출합니다. 입력 한 위치에 가운데 Virtual Earth 컨트롤에서 find (). Virtual earth 맵 서비스 반환 될 때 지도입니다. Find () 메서드를 마지막 인수로 전달 callbackUpdateMapDinners 콜백 메서드를 호출 합니다.

CallbackUpdateMapDinners() 방법은 실제 작업은 수행 하는 위치입니다. JQuery의 $.post() 도우미 메서드를 사용 하 여 위 도와 경도 새로 가운데 맵의 전달이 SearchController SearchByLocation() 동작 메서드에 – AJAX 호출을 수행 합니다. $.Post() 도우미 메서드가 완료 되 면 호출 되는 인라인 함수 정의 및 작업 메서드에 전달 될 "dinners" 라는 변수를 사용 하 여 SearchByLocation()에서 dinner JSON 형식의 결과가 반환 됩니다. 반환 된 각 저녁을 통해 foreach를 수행 하 고 dinner의 위도 및 경도 및 기타 속성을 사용 하 여 지도에 새 pin을를 추가 합니다. 또한 맵의 오른쪽 dinners HTML 목록을 dinner 항목을 추가합니다. 이 다음 와이어 접속 가리키기 이벤트가 압정와 HTML 목록에 대 한 사용자 위로 가져갈 때 dinner에 대 한 세부 정보 표시 되도록:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

및 이제 응용 프로그램을 실행 하 고 맵을 사용 하 여 표시 됩니다 것 홈 페이지 방문 했습니다. 도시 이름을 입력할 때 근처 향후 dinners 지도 표시 됩니다.

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

저녁 식사를 마우스로 가리키면 세부 정보가 표시 됩니다.

Dinner 제목을 클릭 거품 또는 오른쪽에 있는 HTML 목록에는 이동할 우리 dinner –에서는 수 다음 필요에 따라 참석 여부 알림 요청:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>다음 단계

이제 NerdDinner 응용 프로그램의 모든 응용 프로그램 기능을 구현 했습니다. 보겠습니다 이제 자동화 단위 수는 방법을 살펴보겠습니다도 테스트 합니다.

> [!div class="step-by-step"]
> [이전](use-ajax-to-deliver-dynamic-updates.md)
> [다음](enable-automated-unit-testing.md)
