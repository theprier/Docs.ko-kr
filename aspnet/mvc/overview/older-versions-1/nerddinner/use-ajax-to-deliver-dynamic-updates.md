---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX를 사용 하 여 동적 업데이트를 제공 하도록 | Microsoft Docs
author: microsoft
description: 10 단계 구현 dinner 세부 정보에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 사람들이 관심 RSVP에 로그인 한 사용자에 대 한 지원...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 9f11c4c15c0ac9bab8d53b18a4e07be4b864b2c7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825203"
---
<a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX를 사용 하 여 동적 업데이트를 제공 합니다.
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 10 단계인 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 10 단계 구현 dinner 세부 정보 페이지에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 사람들이 관심 RSVP에 로그인 한 사용자에 대 한 지원 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner 10 단계: 않으십니까를 사용 하도록 설정 하는 AJAX 허용

이제 로그인 한 사용자의를 저녁 식사에 참석 사람들이 관심을 회신에 대 한 지원을 구현 해 보겠습니다. 지원할 예정이 dinner 세부 정보 페이지 내에서 통합 된 AJAX 기반 접근 방식을 사용 합니다.

### <a name="indicating-whether-the-user-is-rsvpd"></a>사용자가 주최 하는 여부를 나타내는

사용자가 방문할 수는 */Dinners 세부 정보 / [id*] 특정 저녁에 대 한 세부 정보를 보려면 URL:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

작업 메서드는 구현 Details() 다음과 같이 합니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP 지원을 구현 하기 위해 첫 번째 단계 (내에서 앞서 작성 Dinner.cs 부분 클래스)은 Dinner 개체 "IsUserRegistered(username)" 도우미 메서드를 추가할 수 있습니다. 이 도우미 메서드는 Dinner에 대 한 현재 주최 하는 사용자 여부에 따라 true 또는 false를 반환 합니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

다음 이벤트 또는 하지 Details.aspx 보기 템플릿은 사용자가 등록 되어 있는지 여부를 나타내는 적절 한 메시지를 표시 하려면 다음 코드를 추가할 수 있습니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

고 이제 사용자에 대 한 등록 하는 Dinner 방문이 메시지 볼 수 있습니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

표시에 대 한 등록 하지는 저녁 식사를 방문할 때와 메시지 아래:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Register 작업 메서드를 구현합니다.

세부 정보 페이지에서 사용자는 저녁에 RSVP를 사용 하는 데 필요한 기능을 이제 추가 해 보겠습니다.

이 구현 하려면 만들겠습니다 새 "RSVPController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;컨트롤러 메뉴 명령입니다.

인수로 저녁에는 id를 가져오고, 확인 하 고 경우에 로그인 한 사용자를 등록 하는 사용자 목록에서 현재 경우 적절 한 Dinner 개체를 검색 하는 새 RSVPController 클래스 내에서 "등록" 작업 메서드를 구현 합니다. 에 RSVP 개체를 추가 하지 않습니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

위의 간단한 문자열을 동작 메서드의 출력으로 반환 되는 방법을 확인할 수 있습니다. 이 메시지는 보기 템플릿 내의 포함 수 것 하지만 컨트롤러 기본 클래스에 위의 문자열 메시지와 같은 반환 Content() 도우미 메서드를 사용 작기 때문입니다.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX를 사용 하 여 RSVPForEvent 작업 메서드를 호출

AJAX 사용 하 여 세부 정보 보기에서 등록 동작 메서드를 호출 하겠습니다. 이 구현 하는 것은 매우 쉽습니다. 먼저 두 개의 스크립트 라이브러리 참조 추가 됩니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

핵심 ASP.NET AJAX 클라이언트 쪽 스크립트 라이브러리를 참조 하는 첫 번째 라이브러리입니다. 이 파일 (압축) 크기가 약 24 k 핵심 클라이언트 쪽 AJAX 기능이 포함 되어 있습니다. 두 번째 라이브러리에는 ASP.NET MVC의 기본 제공 AJAX 도우미 메서드 (곧 사용 하겠습니다)와 통합 되는 유틸리티 함수가 포함 됩니다.

RSVP 컨트롤러에서 우리의 RSVPForEvent 작업 메서드를 호출 하는 AJAX 호출을 수행 하는 발견 된 "등록 되지 않습니다이 이벤트에 대 한" 메시지를 대신에서는 대신 렌더링 되도록 링크는 푸시 될 때 이전에 추가한 보기 템플릿 코드를 업데이트 한 다음 수 있습니다. 및 사용자 RSVPs:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

위에서 사용한 Ajax.ActionLink() 도우미 메서드는 ASP.NET MVC에 기본 제공 이며는 Html.ActionLink() 도우미 메서드를 제외 하는 표준 탐색을 수행 하는 대신 있도록 동작 메서드에 대 한 AJAX 호출 링크를 클릭할 때입니다. 위에서 "RSVP" 컨트롤러에서 "Register" 작업 메서드를 호출 하 고를 DinnerID "id" 매개 변수로 전달 합니다. 마지막 AjaxOptions 매개 변수 전달 한다는 동작 메서드에서 반환 된 콘텐츠를 가져와서 HTML을 업데이트 하 &lt;div&gt; id가 "rsvpmsg" 페이지의 요소입니다.

이며 하는 사용자가 탐색할 때에 등록 되지 않은 하 아직 링크에 대 한 RSVP 보게 이제:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

"이이 이벤트에 대 한 RSVP" 링크를 클릭 하는 경우 해당 등록 동작 메서드에 대 한 AJAX 호출 RSVP 컨트롤러에서 만들고 업데이트 된 메시지를 보게 완료 되 면 아래와 같은:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

네트워크 대역폭 및 트래픽이 AJAX 호출을 수행할 때 관련 된 매우 간단한 경우 작은 HTTP POST 네트워크 요청을 사용자가 "RSVP이이 이벤트에 대 한" 링크를 클릭 하려고 합니다 */Dinners/Register/1* URL 유선상 아래 처럼 보이지만입니다.

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

및 Register 작업 메서드는 응답입니다.

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

이 간단한 호출은 속도가 느린 네트워크를 통해도 작동 하며

### <a name="adding-a-jquery-animation"></a>JQuery 애니메이션 추가

AJAX 기능을 구현 했습니다 및 빠른 작동 합니다. 경우에 따라 발생할 수 있습니다 따라서 빠르고 하지만 사용자를 새 텍스트로 RSVP 링크를 교체한을 느끼지 못할 수 있습니다. 업데이트 메시지에 주목 하도록 간단한 애니메이션을 더할 결과 좀 더 명확 하 게 만들 수 있습니다.

기본 ASP.NET MVC 프로젝트 템플릿은 jQuery-microsoft 에서도 지원 되는 뛰어난과 매우 인기 있는 오픈 소스 JavaScript 라이브러리를 포함 합니다. jQuery 다양 한 유용한 HTML DOM 선택 및 효과 라이브러리를 포함 하 여 기능을 제공 합니다.

JQuery를 사용 하려면 먼저 스크립트 참조를 추가 합니다. 때문에 다양 한 위치 내에서 jQuery를 사용 하 여 사이트 내에서 수를 모든 페이지에서 사용할 수 있도록 스크립트 참조가 Site.master 마스터 페이지 파일 내에서 추가 하겠습니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*팁: VS 2008 sp1 JavaScript 파일 (jQuery 포함)에 대 한 다양 한 intellisense를 지 원하는 JavaScript intellisense 핫픽스를 설치 했는지 확인 합니다. 다운로드할 수 있습니다. http://tinyurl.com/vs2008javascripthotfix*

JQuery를 자주 사용 하 여 작성 된 코드는 전역 "$ ()"를 사용 하 여 CSS 선택기를 사용 하 여 하나 이상의 HTML 요소를 검색 하는 JavaScript 메서드. 예를 들어 <em>$("#rsvpmsg")</em> rsvpmsg의 id 사용 하 여 모든 HTML 요소를 선택 하는 동안 <em>$(".something")</em> "휴대 하는 것" CSS를 사용 하 여 모든 요소를 선택 하는 클래스 이름입니다. "Return 모든 선택 된 라디오 단추"와 같은 보다 고급 수준의 쿼리를 작성할 수도 있습니다와 같은 선택기 쿼리를 사용 하 여: <em>$("입력 [@type= 라디오] [@checked]")</em>합니다.

숨기기와 같은 작업을 수행 하도록에서 메서드를 호출 하 여 요소를 선택한 후: *$("#rsvpmsg").hide();*

참석 여부 회신 시나리오에서는 "rsvpmsg"를 선택 하는 "AnimateRSVPMessage" 라는 간단한 JavaScript 함수를 정의 하겠습니다 &lt;div&gt; 해당 텍스트 콘텐츠 크기에 애니메이션 효과 줍니다. 그 다음으로 작은 텍스트 원인 시작 아래 코드는 400 밀리초 시간 지남에 따라 증가할 것:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

우리가 수 다음 실시간 접속 AJAX 호출 이름과 Ajax.ActionLink() 도우미 메서드를 전달 하 여 성공적으로 완료 된 후 호출할 JavaScript 함수가 (AjaxOptions "OnSuccess"를 통해 이벤트 속성):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

이제 "RSVP이이 이벤트에 대 한" 링크를 클릭 하 고 AJAX 호출 완료 되 면 전송 된 메시지 콘텐츠 다시 애니메이션을 적용 되며 커질:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

"OnSuccess" 이벤트를 제공 하는 것 외에도 AjaxOptions 개체는 다양 한 다른 속성 및 유용한 옵션) (함께 처리할 수 있는 OnBegin, OnFailure, 및 OnComplete 이벤트를 노출 합니다.

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>정리-RSVP 부분 보기는 리팩터링

세부 정보 보기 템플릿은 초과 하 게 조금 이해 하기가 약간 긴 하기 시작 합니다. 코드 가독성을 높이기 위해 보겠습니다 가격 세부 정보 페이지에 대 한 RSVP 뷰 코드를 모두 캡슐화 하는 부분 보기 – RSVPStatus.ascx – 만들어 마무리 합니다.

\Views\Dinners 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 추가-이렇게 할&gt;메뉴 명령을 보고 합니다. 해당 강력한 ViewModel로 저녁 식사를 적용 해야 합니다. 에서는 다음 붙여 넣을 수 RSVP 콘텐츠를 Details.aspx 보기에서.

작업을 수행한 후도 보기를 만들어 보겠습니다 다른 부분 – EditAndDeleteLinks.ascx-편집 및 삭제 링크 보기 코드를 캡슐화 하는 합니다. 또한 해야 해당 강력한 ViewModel로 Dinner 개체를 사용 하 고 편집 및 삭제 논리를 Details.aspx 보기에서 복사/붙여넣기.

정보의는 템플릿 수를 확인 한 후 바로 아래에 두 Html.RenderPartial() 메서드 호출을 포함 합니다.

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

이렇게 하면 코드를 더 깔끔하게 읽고 유지 관리 합니다.

### <a name="next-step"></a>다음 단계

이제 살펴보겠습니다 것을 수 있는 방법은 더욱 AJAX를 사용 하 여 응용 프로그램에 대화형 매핑 지원을 추가 합니다.

> [!div class="step-by-step"]
> [이전](secure-applications-using-authentication-and-authorization.md)
> [다음](use-ajax-to-implement-mapping-scenarios.md)
