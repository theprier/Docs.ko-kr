---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: "AJAX를 사용 하 여 동적 업데이트를 제공 하도록 | Microsoft Docs"
author: microsoft
description: "자신의 관심사 dinner 세부 정보에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 RSVP에 로그인 한 사용자에 대 한 지원을 10 단계 구현 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 7b75f8c6cf08112eb77d1a9a40222ed1425ef3a7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX를 사용 하 여 동적 업데이트를 제공 하려면
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 10 단계인 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 자신의 관심사 dinner 세부 정보 페이지에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 RSVP에 로그인 한 사용자에 대 한 지원을 10 단계 구현 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>업그레이드 되었으며 수정 10 단계: 않으십니까를 사용 하도록 설정 하는 AJAX 허용

이제 로그인 한 사용자는 저녁 참석 자신의 관심사 RSVP에 대 한 지원을 구현 해 보겠습니다. 활성화이 dinner 세부 정보 페이지에 통합 하는 AJAX 기반 접근 방식을 사용 합니다.

### <a name="indicating-whether-the-user-is-rsvpd"></a>사용자가 주최 있는지 여부를 나타내는

사용자가 방문할 수는 */Dinners/세부 정보 / [id*] 특정 저녁에 대 한 자세한 내용을 보려면 URL:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

동작 메서드는 구현 Details() 같이:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP 지원을 구현 하기 위해 첫 번째 단계 (내에서 앞에서 만든 partial Dinner.cs 클래스) 우리의 Dinner 개체는 "IsUserRegistered(username)" 도우미 메서드를 추가 됩니다. 이 도우미 메서드는 true 또는 사용자는 저녁에 주최 현재가 있는지 여부에 따라 false를 반환 합니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

그런 다음 이벤트에 대해 화는 사용자가 등록 되어 있는지 여부를 나타내는 적절 한 메시지를 표시 하는 Details.aspx 보기 서식 파일에 다음 코드를 추가할 수 있습니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

고 이제 사용자에 대해 등록 된 저녁에 방문할 때이 메시지가 표시 됩니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

표시에 대 한 등록 되지 않은 Dinner를 방문 하 고는 아래 메시지가:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Register 작업 메서드를 구현합니다.

세부 정보 페이지에서 사용자는 저녁에 RSVP를 사용 하는 데 필요한 기능을 이제 추가 해 보겠습니다.

이 구현 하려면 만들겠습니다 새 "RSVPController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가 기능 선택 하 여&gt;컨트롤러 메뉴 명령입니다.

확인 하 고, 등록 한 사용자 목록에 로그인 한 사용자는 현재 고 하는 경우 적절 한 Dinner 개체를 검색에 대 한 인수로 서 Dinner id를 사용 하는 새 RSVPController 클래스 내에서 "Register" 작업 메서드 구현 RSVP 개체를 추가 하지 않습니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

위의 간단한 문자열 동작 메서드의 출력으로 반환 되는 방법을 확인 합니다. 내 보기 템플릿의 경우-이 메시지를 삽입 한 수 우리 하지만 비율은 매우 작으므로 이후 방금에서는 Content() 도우미 메서드 위에 문자열 메시지와 같은 돌아가 컨트롤러 기본 클래스에서.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX를 사용 하 여 RSVPForEvent 동작 메서드 호출

이 세부 정보 보기에서 레지스터 동작 메서드를 호출 하 AJAX를 사용 합니다. 이 구현 하는 것은 아주 간단 합니다. 먼저 두 개의 스크립트 라이브러리 참조를 추가 합니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

첫 번째 라이브러리 핵심 ASP.NET AJAX 클라이언트 쪽 스크립트 라이브러리를 참조합니다. 이 파일 (압축) 크기의 약 24 k 하며 핵심 클라이언트 쪽 AJAX 기능을 포함 합니다. 두 번째 라이브러리는 ASP.NET MVC의 기본 제공 AJAX 도우미 메서드 (에서는 곧)와 통합 하는 유틸리티 함수를 포함 합니다.

활용해 서 RSVP controller에서 우리의 RSVPForEvent 작업 메서드를 호출 하는 AJAX 호출을 수행 하는 "하면 등록 되지 않은이 이벤트에 대 한" 메시지 outputing 대신 우리 대신 링크를 렌더링 하는 푸시 되도록 앞서 추가 보기 템플릿 코드를 업데이트 한 다음 및 사용자 RSVPs:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

위에서 사용한 Ajax.ActionLink() 도우미 메서드는 ASP.NET MVC에 기본 제공 이며는 Html.ActionLink() 도우미 메서드를 제외 하는 표준 탐색을 수행 하는 대신는 동작 메서드에 대 한 AJAX 호출 링크를 클릭할 때입니다. 위의 "RSVP" 컨트롤러에서 "Register" 동작 메서드를 호출 하 고를 DinnerID "id" 매개 변수로 전달 합니다. 마지막 위해 AjaxOptions 매개 변수 전달 한다는 동작 메서드에서 반환 된 콘텐츠를 HTML 업데이트 &lt;div&gt; id가 "rsvpmsg" 페이지에서 요소입니다.

이며 사용자가을 dinner를 찾을 때에 대 한 등록 되어 있지 않습니다 하 아직 RSVP에 대 한 링크를 볼 수 있습니다 이제:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

레지스터 동작 메서드에 대 한 AJAX 호출 RSVP 컨트롤러에서 만드는 합니다 "RSVP이이 이벤트에 대 한" 링크를 클릭 하 고 작업이 완료 될 때 업데이트 된 메시지가 표시 됩니다 다음과 유사한:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

네트워크 대역폭 및 트래픽이 AJAX 호출을 수행 하는 경우 관련 되는 가벼운입니다. 에 대 한 작은 HTTP POST 네트워크 요청이 사용자가 "RSVP이이 이벤트에 대 한" 링크를 클릭 하면는 */Dinners/Register/1* 통신 중에 아래 다음과 같은 URL:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

그리고이 레지스터 작업 메서드에서 응답 단순히:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

이 간단한 호출은 신속 하 고 느린 네트워크를 통해 작동 합니다.

### <a name="adding-a-jquery-animation"></a>JQuery 애니메이션 추가

AJAX 기능을 구현 했습니다 빠른 및 잘 작동 합니다. 경우에 따라 발생할 수 있습니다 너무를 빨리 하지만 사용자를 새 텍스트로 RSVP 링크 바뀌었음을 느끼지 못할 수 있습니다. 결과 좀 더 명확 하 게 하려면 업데이트 메시지에 주목 하도록 간단한 애니메이션을 추가할 수 있습니다.

기본 ASP.NET MVC 프로젝트 템플릿에 jQuery – Microsoft에서 에서도 지원 되는 뛰어난 (및 인기 있는) 오픈 소스 JavaScript 라이브러리를 포함 합니다. jQuery는 다양 한 기능을 갖춰 바로 HTML DOM 선택 및 효과 라이브러리를 포함 하 여 제공 합니다.

JQuery를 사용 하려면 먼저 스크립트 참조를 추가 합니다. 사이트 내에서 다양 한 위치 내에서 jQuery 사용할 것 이며, 때문에 모든 페이지에서 사용할 수 있도록 스크립트 참조 우리의 Site.master 마스터 페이지 파일 내에서 추가 합니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*팁: JavaScript 파일 (jQuery 포함)에 대 한 보다 다양 한 intellisense 지원을 VS 2008 s p 1에 대 한 JavaScript intellisense 핫픽스를 설치 했는지 확인 합니다. 다운로드할 수 있습니다: http://tinyurl.com/vs2008javascripthotfix*

종종 JQuery를 사용 하 여 작성 된 코드는 전역 "$ ()"를 사용 하 여 CSS 선택기를 사용 하 여 하나 이상의 HTML 요소를 검색 하는 JavaScript 메서드. 예를 들어 *$("#rsvpmsg")* rsvpmsg id로 HTML 요소를 선택 하는 동안 *$(".something")* "어떤 항목" CSS 갖는 모든 요소 선택 클래스 이름입니다. "Return 모든 선택 된 라디오 단추"와 같은 보다 고급 수준의 쿼리를 작성할 수도 있습니다 같은 선택기 쿼리를 사용 하 여: *$("입력 [@type라디오 =] [@checked]")*합니다.

숨기기와 같은 작업을 수행할 수 있는 메서드를 호출할 수 요소를 선택한 후: *$("#rsvpmsg").hide();*

RSVP 시나리오에 대 한 "rsvpmsg" 선택 "AnimateRSVPMessage" 라는 간단한 JavaScript 함수 정의 하겠습니다 &lt;div&gt; 하 고 해당 텍스트 내용의 크기를 애니메이션 합니다. 작은 텍스트와 다음 원인 시작 아래 코드는 400 밀리초 기간을 통해 향상을 위해:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

म 수 다음 실시간 접속이 JavaScript 함수 우리의 AJAX 호출 Ajax.ActionLink() 도우미 메서드를 해당 이름을 전달 하 여 성공적으로 완료 된 후에 호출 수입니다 (위해 AjaxOptions "OnSuccess"를 통해 이벤트 속성):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

이제 "RSVP이이 이벤트에 대 한" 링크를 클릭 하 고이 AJAX 호출이 완료 되 면 전송 되는 콘텐츠 메시지 다시 애니메이션 효과 적용 되며 커질:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

"OnSuccess" 이벤트를 제공할 뿐만 아니라 위해 AjaxOptions 개체는 다양 한 다른 속성 및 유용한 옵션) (함께 처리할 수 있는 OnBegin, OnFailure, 및 OnComplete 이벤트를 노출 합니다.

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>정리-RSVP 부분 뷰 아웃 리팩터링

이 세부 정보 보기 템플릿 어떤 초과 더 어려워지며 조금 이해 하 약간 길어질를 시작 합니다. 코드 가독성을 향상 시키려면 보겠습니다 가격 세부 정보 페이지에 대 한 RSVP 보기 코드를 모두 캡슐화 하는 부분 뷰 – RSVPStatus.ascx – 만들어 마무리 합니다.

\Views\Dinners 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 추가-이렇게 하려면&gt;보기 메뉴 명령입니다. म Dinner 개체의 강력한 형식의 ViewModel으로 사용 하도록 합니다. म 수 다음 복사/붙여넣기 RSVP 콘텐츠에서 우리의 Details.aspx 뷰입니다.

작업을 수행한 후도 보기를 만들어 보겠습니다 다른 부분 – EditAndDeleteLinks.ascx-편집 및 삭제 링크 보기 코드를 캡슐화 하 합니다. 저녁 개체의 강력한 형식의 ViewModel으로 사용 되어 있고 복사/붙여넣기를 우리의 Details.aspx 뷰가에서 편집 및 삭제 논리 해야 합니다.

이 세부 정보 템플릿 수를 확인 한 후 바로 아래에 두 개의 Html.RenderPartial() 메서드 호출을 포함:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

그러면 코드를 읽고 유지 관리 정리 합니다.

### <a name="next-step"></a>다음 단계

이제 살펴보겠습니다 AJAX를 사용 하 여 더욱 해소를 응용 프로그램에 대화형 매핑 지원을 추가할 수 있습니다 어떻게.

>[!div class="step-by-step"]
[이전](secure-applications-using-authentication-and-authorization.md)
[다음](use-ajax-to-implement-mapping-scenarios.md)
