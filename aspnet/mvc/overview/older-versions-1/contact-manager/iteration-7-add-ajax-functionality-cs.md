---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: '반복 #7 – Ajax 기능 추가 (C#) | Microsoft Docs'
author: microsoft
description: 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: 9b7a3acefbfeef9da5e45b40f03809b00364de05
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396158"
---
<a name="iteration-7--add-ajax-functionality-c"></a>반복 #7 – Ajax 기능 추가 (C#)
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (C#)

이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다. 연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.

여러 반복에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-보기 좋게 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 네 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 #6-테스트 중심 개발을 사용 합니다. 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.

- 반복 #7 – Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

연락처 관리자 응용 프로그램의이 반복에서 Ajax를 활용 하도록 응용 프로그램을 리팩터링 했습니다. Ajax를 활용 하 여 우리가 응용 프로그램 응답성이 향상 됩니다. 에서는 페이지에 특정 지역 에서만 업데이트 해야 할 때 전체 페이지 렌더링을 방지할 수 있습니다.

인덱스 보기 할 필요도 새 연락처 그룹을 선택할 때마다 전체 페이지를 다시 표시 하지 것 하도록 리팩터링 됩니다 것입니다. 대신 메일 그룹을 클릭할 때 것만 연락처 목록을 업데이트 하 고 페이지의 나머지 부분을 단독으로 그대로 둡니다.

또한이 삭제 링크 작동 방식에서는 변경 합니다. 별도 확인 페이지를 표시 하는 대신 JavaScript 확인 대화 상자가 표시 됩니다. 연락처 삭제 되도록 확인 하는 경우 연락처 레코드를 데이터베이스에서 삭제 하는 서버에 대해 HTTP DELETE 작업 수행 됩니다.

게다가 우리가 이용 하는 인덱스 보기에 애니메이션 효과 추가 하려면 jQuery의 합니다. 새 연락처 목록을 서버에서 인출 되는 경우 애니메이션을 표시 됩니다.

마지막으로 ASP.NET AJAX 프레임 워크는 브라우저 기록을 관리 하는 것에 대 한 지원 기능을 알아보겠습니다. 연락처 목록을 업데이트 하는 Ajax 호출이 수행 될 때마다 기록 점을 만들어 보겠습니다. 이런 방식으로 브라우저 뒤로 및 앞으로 단추는 작동 합니다.

## <a name="why-use-ajax"></a>Ajax를 사용 하는 이유는?

Ajax를 사용 하 여 많은 장점이 있습니다. 먼저 더 나은 사용자 환경은 응용 프로그램에 Ajax 기능을 추가 합니다. 일반 웹 응용 프로그램에서 전체 페이지를 게시 해야 서버에 사용자 작업을 수행 하는 각 시간입니다. 작업을 수행할 때마다 브라우저 잠금과 사용자 전체 페이지를 인출 하 고 다시 표시 될 때까지 대기 해야 합니다.

이 데스크톱 응용 프로그램의 경우 허용 되지 않는 환경을 것입니다. 하지만 일반적으로 우리 수명이 웹 응용 프로그램의 경우이 안 좋은 사용자 환경을 더 잘 우리가 알지 못했던 때문입니다. 생각 했을 때, 실제로 imaginations에 대 한 제한만 웹 응용 프로그램에 대 한 제한 된 합니다.

Ajax 응용 프로그램에서는 페이지 업데이트를 중단 하는 사용자 경험을 t 필요를 하지 있습니다. 대신 페이지 업데이트는 백그라운드에서 비동기 요청을 수행할 수 있습니다. 사용자가 페이지의 부분 업데이트 하는 동안 기다려야 t 강제 하지.

Ajax를 활용 하 여도 응용 프로그램의 성능이 향상 수 있습니다. 연락처 관리자 응용 프로그램의 작동 원리 지금 당장 Ajax 기능 없이 하는 것이 좋습니다. 문의 그룹을 클릭 하면 전체 인덱스 뷰에 다시 표시 해야 합니다. 데이터베이스 서버에서 연락처 목록과 연락처 그룹 목록을 검색 해야 합니다. 이 모든 데이터를 전달 해야 네트워크를 통해 웹 서버에서 웹 브라우저입니다.

그러나 Ajax 기능을 응용 프로그램을 추가한 후에서는 방지할 수 있습니다 연락처 그룹을 클릭할 때 전체 페이지를 표시 합니다. 더 이상 데이터베이스에서 메일 그룹을 선택 해야 합니다. 에서는 네트워크를 통해 전체 인덱스 뷰를 푸시할 필요가 t도 하지. Ajax를 활용 하 여 데이터베이스 서버에서 수행 해야 하는 작업량이 줄어듭니다 및 응용 프로그램에 필요한 네트워크 트래픽 양을 줄입니다.

## <a name="don-t-be-afraid-of-ajax"></a>안 될 두려워의 Ajax

일부 개발자는 하위 브라우저에 대 한 걱정 때문에 Ajax를 사용 하지 마십시오. JavaScript를 지원 하지 않는 브라우저에서 액세스할 때 웹 응용 프로그램은 계속 작동 하는지 확인 하려고 합니다. Ajax JavaScript에 의존 하기 때문에 일부 개발자 들은 Ajax를 사용 하지 마십시오.

그러나 Ajax를 구현 하는 방법에 대 한 주의 상위 및 하위 브라우저는 응용 프로그램을 빌드할 수 있습니다. 연락처 관리자 응용 프로그램은 JavaScript를 지 원하는 브라우저 및 하지 않는 브라우저를 사용 하 여 작동 합니다.

JavaScript를 지 원하는 브라우저를 사용 하 여 연락처 관리자 응용 프로그램을 사용 하면 더 나은 사용자 환경을 합니다. 예를 들어, 메일 그룹을 클릭 하면 연락처를 표시 하는 페이지의 영역에만 업데이트 됩니다.

브라우저 JavaScript를 지원 하지 않는 (또는 사용 하지 않도록 설정 하는 JavaScript 포함)를 사용 하 여 연락처 관리자 응용 프로그램을 사용 하는 반면, 하는 경우 하면 약간 그다지 사용자 경험을 합니다. 예를 들어, 메일 그룹을 클릭 하면 전체 인덱스 보기 게시 해야 브라우저를 다시 일치 하는 연락처 목록을 표시 하기 위해.

## <a name="adding-the-required-javascript-files"></a>필요한 JavaScript 파일 추가

세 개의 JavaScript 파일을 사용 하 여 응용 프로그램에 Ajax 기능을 추가 해야 합니다. 이러한 파일의 세 가지를 모두 새 ASP.NET MVC 응용 프로그램의 스크립트 폴더에 포함 됩니다.

응용 프로그램의 여러 페이지에서 Ajax를 사용 하려는 경우 다음 편이 응용 프로그램의 보기 마스터 페이지에 필요한 JavaScript 파일을 포함 합니다. 이런 방식으로 JavaScript 파일은 모든 응용 프로그램에서 페이지의 자동으로 포함 합니다.

내에 포함 되어 다음과 같은 JavaScript를 추가 합니다 &lt;head&gt; 보기 마스터 페이지의 태그:

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Ajax를 사용 하도록 인덱스 뷰 리팩터링

S를 인덱스 보기 수정 연락처를 표시 하는 보기의 영역을 업데이트만 연락처 그룹을 클릭 하 여 시작할 수 있습니다. 그림 1에 빨간색 상자 업데이트 하고자 하는 영역을 포함 합니다.


[![만 연락처를 업데이트 하는 중](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)

**그림 01**:만 연락처를 업데이트 하는 중 ([큰 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-cs/_static/image2.png))


첫 번째 단계는 별도 부분 (뷰 사용자 컨트롤)를 비동기적으로 업데이트 하려는 보기의 일부를 분리 하는 것입니다. 연락처의 테이블을 표시 하는 인덱스 뷰의 섹션 목록 1에서 부분으로 이동 되었습니다.

**Listing 1 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

목록 1에서 부분 인덱스 보기 보다 다른 모델에 있는지 확인 합니다. *Inherits* 특성을 &lt;페이지 % @ %&gt; 지시문 부분을 ViewUserControl에서 상속 되도록 지정&lt;그룹&gt; 클래스입니다.

업데이트 된 인덱스 뷰는 목록 2에 포함 됩니다.

**Listing 2 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

목록 2에서 업데이트 된 보기에 대 한 유의 해야 하는 방법은 두 가지 있습니다. 첫째, 콘텐츠의 모든 부분으로 이동 하는 알림 Html.RenderPartial()에 대 한 호출으로 대체 됩니다. Html.RenderPartial() 메서드는 인덱스 보기 연락처의 초기 집합을 표시 하려면 먼저 요청 될 때 호출 됩니다.

둘째, 메일 그룹을 표시 하는 데는 Html.ActionLink()는 Ajax.ActionLink()를 사용 하 여 대체 되었습니다. 다음 매개 변수를 사용 하 여는 Ajax.ActionLink() 라고 합니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

첫 번째 매개 변수 링크에 대해 표시할 텍스트를 나타내는, 두 번째 매개 변수가 나타내는 경로 값 및 세 번째 매개 변수는 Ajax 옵션을 나타냅니다. 이 경우 HTML를 가리키도록 UpdateTargetId Ajax 옵션을 사용 했습니다 &lt;div&gt; Ajax 요청이 완료 된 후 업데이트 하고자 하는 태그입니다. 업데이트 하고자 합니다 &lt;div&gt; 새 연락처 목록 사용 하 여 태그입니다.

연락처 컨트롤러의 업데이트 된 index () 메서드는 목록 3에 포함 됩니다.

**3-Controllers\ContactController.cs (인덱스 메서드)를 나열합니다.**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

조건에 따라 업데이트 된 index () 작업을 두 가지 중 하나를 반환합니다. Index () 작업은 Ajax 요청에 의해 호출 되 면 컨트롤러 부분을 반환 합니다. Index () 작업, 전체 뷰를 반환합니다.

알림 index () 작업 Ajax 요청에 의해 호출 될 때 많은 데이터를 반환할 필요가 없습니다. 일반 요청 컨텍스트에서 인덱스 작업에는 모든 연락처 그룹 및 선택한 연락처 그룹의 목록을 반환합니다. Ajax 요청의 컨텍스트에 index () 작업에는 선택한 그룹에만 반환합니다. Ajax는 데이터베이스 서버에서 더 적은 작업을 의미합니다.

수정 된 인덱스 뷰에 상위 및 하위 브라우저의 경우 작동합니다. 문의 그룹을 클릭 하면 브라우저에서 JavaScript를 지원 하 고 연락처 목록을 포함 하는 뷰의 지역만 업데이트 됩니다. 반면에 브라우저가 JavaScript를 지원 하지 않습니다, 경우에 전체 뷰가 업데이트 됩니다.


업데이트 된 인덱스 보기 한 가지 문제가 있습니다. 문의 그룹을 클릭 하면 선택한 그룹을 강조 표시 되지 않습니다. Ajax 요청 중에 업데이트 되는 지역 외부에 있는 그룹의 목록이 표시 됩니다, 때문에 올바른 그룹을 강조 표시 가져오기지 않습니다. 다음 섹션에서이 문제를 해결할 예정입니다.


## <a name="adding-jquery-animation-effects"></a>JQuery 애니메이션 효과 추가합니다.

일반적으로 웹 페이지의 링크를 클릭 하면 브라우저를 적극적으로 업데이트 된 콘텐츠를 페치하는 여부를 검색할 브라우저 진행률 표시줄을 사용할 수 있습니다. Ajax 요청을 수행할 때 다른 한편으로 브라우저 진행률 표시줄이 표시 되지 않습니다에 있어서 어떠한 진전이. 이 가능 사용자 우려 합니다. 브라우저에 고정 되어 있는지를 어떻게 알 수 있을까요?

Ajax 요청을 수행 하는 동안 작업이 수행 되는 사용자를 나타낼 수 있는 방법은 여러 가지가 있습니다. 한 가지 방법은 간단한 애니메이션을 표시 하는 것입니다. 예를 들어, Ajax 요청을 시작 하 고 요청이 완료 되 면 지역에서 페이드 인 경우 영역 아웃 페이드 수 있습니다.

애니메이션 효과를 만들 Microsoft ASP.NET MVC framework에 포함 된 jQuery 라이브러리를 사용 하겠습니다. 업데이트 된 인덱스 뷰 목록 4에 포함 됩니다.

**Listing 4 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

업데이트 된 인덱스 뷰 세 개의 새 JavaScript 함수에 알 수 있습니다. 처음 두 함수 페이드 아웃 하는 새 메일 그룹을 클릭 하면 연락처 목록의 페이드 jQuery를 사용 합니다. 세 번째 함수 오류가 (예: 네트워크 시간 초과)는 오류 메시지가 나타난다는 Ajax 요청 결과 표시 합니다.

또한 첫 번째 함수는 선택한 그룹을 강조 표시의 담당 합니다. 클래스 = 선택한 특성은 클릭 한 요소의 상위 요소 (LI 요소)에 추가 됩니다. 다시, jQuery 쉽게 적합 한 요소를 선택 하 고 CSS 클래스를 추가 합니다.

이러한 스크립트는 Ajax.ActionLink() AjaxOptions 매개 변수를 사용 하 여 그룹 링크에 연결 됩니다. 업데이트 된 Ajax.ActionLink() 메서드 호출이 다음과 유사합니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>브라우저 기록 지원 추가

일반적으로 페이지 업데이트에 대 한 링크를 클릭 하면 브라우저 기록 업데이트 됩니다. 이런 방식으로 페이지의 이전 상태 시간에서 다시 이동 하려면 브라우저의 뒤로 단추를 클릭 수 있습니다. 예를 들어, 친구 문의 그룹을 클릭 하 고 비즈니스 연락처 그룹을 클릭 하는 경우에 친구 문의 그룹을 선택 하는 경우 페이지의 상태를 다시 탐색 하 브라우저 뒤로 단추를 클릭 수 있습니다.

그러나 Ajax 요청을 수행 합니다. 업데이트 하지 않습니다 브라우저 기록을 자동으로. 문의 그룹을 클릭 하 고 Ajax 요청을 사용 하 여 연락처를 일치 하는 목록을 검색 하는 경우 브라우저 기록을 업데이트 되지 않습니다. 브라우저의 뒤로 단추를 사용 하 여 새 연락처 그룹을 선택한 후 메일 그룹으로 이동할 수 없습니다.

하려는 경우 사용자가 브라우저를 다시 사용할 수 있도록 단추 Ajax 요청을 수행한 후 좀 더 많은 작업을 수행 해야 합니다. ASP.NET AJAX 프레임 워크에 기본 제공 브라우저 기록 관리 기능을 활용 해야 합니다.

ASP.NET AJAX 브라우저 기록 등에 세 가지를 수행 해야 합니다.

1. 브라우저 기록 enableBrowserHistory 속성을 true로 설정 하 여 사용 합니다.
2. 뷰 상태가 변경 addHistoryPoint() 메서드를 호출 하 여 기록 점을 저장 합니다.
3. 탐색 이벤트가 발생할 때 뷰의 상태를 다시 생성 합니다.

업데이트 된 인덱스 뷰 목록 5에 포함 됩니다.

**Listing 5 - Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

목록 5 브라우저 기록 pageInit() 함수에서 사용 됩니다. PageInit() 함수 navigate 이벤트에 대 한 이벤트 처리기를 설정도 사용 됩니다. 브라우저 앞으로 또는 뒤로 단추 상태 변경 하려면 페이지를 발생 시킬 때마다 navigate 이벤트를 발생 합니다.

BeginContactList() 메서드 연락처 그룹을 클릭할 때 호출 됩니다. 이 메서드는 새 기록 점을 addHistoryPoint() 메서드를 호출 하 여 만듭니다. 클릭 하면 연락처 그룹의 id 기록에 추가 됩니다.

그룹 id는 연락처 그룹 링크에 대 한 expando 특성에서 검색 됩니다. 링크는 Ajax.ActionLink() 다음 호출을 사용 하 여 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

마지막 매개 변수는 Ajax.ActionLink() 전달할 groupid 링크 (XHTML 호환성을 위해 소문자) 라는 expando 특성을 추가 합니다.

사용자 브라우저의 뒤로 또는 앞으로 단추에 도달 하면 탐색 이벤트가 발생 하 고 navigate() 메서드를 호출 합니다. 이 메서드는 navigate 메서드를 전달 하는 브라우저 기록 지점에 해당 하는 페이지의 상태와 일치 하도록 페이지에 표시 된 연락처를 업데이트 합니다.

## <a name="performing-ajax-deletes"></a>Ajax를 수행 하면 삭제

현재 연락처를 삭제 하기 위해 해야 할 삭제 링크를 클릭 하 고 삭제 확인 페이지에 표시 된 삭제 단추를 클릭 (그림 2 참조). 이 페이지 요청 데이터베이스 레코드가 삭제와 같은 간단한 작업을 수행 하려면 많은 것 같습니다.


[![삭제 확인 페이지](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)

**그림 02**: 삭제 확인 페이지 ([큰 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-cs/_static/image4.png))


삭제 확인 페이지를 건너뛰고 인덱스 보기에서 직접 연락처를 삭제 하기 쉽습니다. 응용 프로그램 보안 취약점을 열어이 접근 방식을 때문에이 유혹을 피해 야 합니다. 일반적으로 don t 웹 응용 프로그램의 상태를 수정 하는 작업을 호출할 때 HTTP GET 작업을 수행 하려고 합니다. 삭제를 수행할 때 HTTP POST를 수행 하거나 HTTP DELETE 작업 하려는 합니다.

삭제 링크를 부분 ContactList에 포함 됩니다. 업데이트 된 부분 ContactList 목록 6에 포함 됩니다.

**Listing 6 - Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

삭제 링크를 Ajax.ImageActionLink() 메서드에 다음 호출을 사용 하 여 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> ASP.NET MVC framework의 표준 파트를 Ajax.ImageActionLink() 아닙니다. Ajax.ImageActionLink() Contact Manager 프로젝트에 포함 하는 사용자 지정 도우미 메서드는입니다.


AjaxOptions 매개 변수는 다음과 같은 두 가지 속성이 있습니다. 먼저 확인 속성 팝업 JavaScript 확인 대화 상자를 표시 됩니다. 둘째, HttpMethod 속성은 HTTP DELETE 작업 수행을 위해 사용 됩니다.

코드 7 연락처 컨트롤러에 추가 된 새 AjaxDelete() 동작을 포함 합니다.

**7-Controllers\ContactController.cs (AjaxDelete)를 나열합니다.**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

AjaxDelete() 작업 AcceptVerbs 특성으로 데코레이팅됩니다. 이 특성의 HTTP 삭제 작업 외의 모든 HTTP 작업에서 제외 하 고 호출 될 작업을 방지 합니다. 특히 HTTP GET을 사용 하 여이 작업을 호출할 수 없습니다.

데이터베이스 레코드를 삭제 하면 삭제 된 레코드는 포함 되지 않은 연락처의 업데이트 된 목록을 표시 해야 합니다. AjaxDelete() 메서드는 부분 ContactList 및 업데이트 된 연락처 목록을 반환합니다.

## <a name="summary"></a>요약

이 반복에서 연락처 관리자 응용 프로그램에 Ajax 기능을 추가 했습니다. 응용 프로그램의 성능과 응답성을 개선 하기 위해 Ajax를 사용 했습니다.

첫째, 두 번 클릭 하면 연락처 전체 보기를 업데이트 하지 않습니다 있도록 인덱스 보기를 리팩터링 했습니다. 대신, 연락처 목록을 업데이트만 연락처 그룹을 클릭 합니다.

다음으로, jQuery 애니메이션 효과 연락처 목록에 페이드 인 및 페이드 아웃을 사용 했습니다. Ajax 응용 프로그램에 애니메이션 추가 브라우저 진행률 표시줄의 해당 하는 응용 프로그램의 사용자에 게 제공 하려면 사용할 수 있습니다.

또한 브라우저 기록 지원 Ajax 응용 프로그램을 추가 했습니다. 사용자가 브라우저의 뒤로 클릭 합니다. 앞으로 인덱스 뷰의 상태를 변경 하는 단추를 사용 하도록 설정 했습니다.

마지막으로, HTTP DELETE 작업을 지 원하는 삭제 링크를 만들었습니다. Ajax 삭제를 수행 하 여 사용자 추가 삭제 확인 페이지를 요청 하도록 요구 하지 않고 데이터베이스 레코드를 삭제 하는 사용자 설정 합니다.

> [!div class="step-by-step"]
> [이전](iteration-6-use-test-driven-development-cs.md)
> [다음](iteration-1-create-the-application-vb.md)
