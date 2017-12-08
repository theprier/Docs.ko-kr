---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: "반복 #7 – 추가 Ajax 기능 (VB) | Microsoft Docs"
author: microsoft
description: "일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: fa50fdea8ac165be3f8e96322ec049196a511ebe
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="iteration-7--add-ajax-functionality-vb"></a>반복 #7 – 추가 Ajax 기능 (VB)
====================
여 [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램 (VB) 빌드
  

이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다. 관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.

여러 반복을 통해에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-모양이 아닌 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-폼 유효성 검사를 추가 합니다. 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 6-테스트 기반 개발을 사용 합니다. 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

이 반복 않아 응용 프로그램에서 Ajax를 사용 하려면 응용 프로그램을 리팩터링한 합니다. Ajax 활용 하도록 응용 프로그램 응답성. 전체 페이지를 렌더링 하는 페이지의 특정 영역 에서만 업데이트 해야 할 때를 방지할 수 있습니다.

됩니다 리팩터링한 우리의 인덱스 뷰 할 필요도 다른 사용자가 새 메일 그룹을 선택할 때마다 전체 페이지를 다시 표시 하지 않는 것에 있도록 합니다. 대신, 메일 그룹을 클릭할 때 방금 연락처 목록 업데이트 알아보고 하겠습니다 페이지의 나머지를 단독으로 둡니다.

또한 우리의 delete 연결의 작동 방식을 변경 합니다. 별도 확인 페이지를 표시 하는 대신 JavaScript 확인 대화 상자를 표시 합니다. 연락처 삭제 되도록 확인 하면 HTTP DELETE를 수행 하는 데이터베이스에서 연락처 레코드를 삭제 하는 서버에 대해 수행 됩니다.

또한 활용 jQuery 우리의 인덱스 보기에 애니메이션 효과 추가 하려면 해당 메뉴로 이동 합니다. 서버에서 새 연락처 목록을 가져온 되 고 애니메이션을 표시 합니다.

마지막으로, ASP.NET AJAX 프레임 워크는 브라우저 기록을 관리에 대 한 지원 기능을 이동 합니다. 연락처 목록 업데이트 하기 위해 Ajax 호출이 수행 될 때마다 기록 점을 만들어 보겠습니다. 이런 방식으로 브라우저 뒤로 및 앞으로 단추는 작동 합니다.

## <a name="why-use-ajax"></a>Ajax를 사용 하는 이유는?

Ajax 사용 하 여 많은 장점이 있습니다. 첫째, 더 나은 사용자 환경은 응용 프로그램에 Ajax 기능을 추가합니다. 일반 웹 응용 프로그램에서는 페이지 전체 게시 해야 서버에는 작업을 수행 하는 각 시간입니다. 작업을 수행할 때마다 브라우저 잠금과 사용자 전체 페이지를 인출 하 고 다시 표시 될 때까지 대기 해야 합니다.

이 데스크톱 응용 프로그램의 경우 허용 되지 않는 경험 것입니다. 그러나 일반적으로 우리 동안 활성 상태로 유지이 잘못 된 사용자 환경을 웹 응용 프로그램의 경우 모든 좋음 우리가 할 수 있는 알지 못했지만 때문에 있습니다. 웹 응용 프로그램의 제한 되었을 때 되었을 뿐 우리 imaginations 제한인 실제로 우리 생각할 수 있습니다.

Ajax 응용 프로그램에서 자신에 게 맞는 t 사용자 환경 페이지 업데이트를 중지 상태로 전환 해야 합니다. 대신, 페이지를 업데이트 하는 백그라운드에서 비동기 요청을 수행할 수 있습니다. 자신에 게 맞는 t force 가져옵니다는 페이지의 일부를 업데이트 하는 동안 대기 하는 사용자입니다.

Ajax 활용 함으로써도 향상 시킬 수 있습니다 응용 프로그램의 성능을 합니다. 않아 응용 프로그램 현재 Ajax 기능 없이 작동 방법을 고려 합니다. 메일 그룹을 클릭할 때 전체 인덱스 뷰 다시 표시 해야 합니다. 연락처 목록 및 메일 그룹의 목록을 데이터베이스 서버에서 검색 해야 합니다. 이 모든 데이터를 전달 해야 네트워크를 통해 웹 서버에서 웹 브라우저입니다.

그러나 응용 프로그램에 Ajax 기능을 추가 했습니다 우리 방지할 수 연락처 그룹을 클릭할 때 전체 페이지를 다시 표시 합니다. 더 이상 데이터베이스에서 메일 그룹을 선택 해야 합니다. T가 전체 인덱스 뷰를 통해 푸시 필요가 또한 하지 않는 합니다. Ajax 활용 함으로써 데이터베이스 서버에 수행 해야 하는 작업의 양을 줄입니다 및 응용 프로그램에 필요한 네트워크 트래픽의 양을 줄입니다.

## <a name="don-t-be-afraid-of-ajax"></a>안 두려워의 Ajax 수

일부 개발자가 하위 브라우저 걱정할 것 때문에 Ajax를 사용 하지 마십시오. JavaScript를 지원 하지 않는 브라우저에서 액세스 하면 해당 웹 응용 프로그램은 계속 작동 하 고 있는지 확인 하려고 합니다. Ajax JavaScript에 의존 하기 때문에 일부 개발자 Ajax를 사용 하지 마십시오.

그러나 Ajax를 구현 하는 방법에 대 한 주의 않으면 상위 및 하위 수준 모두 브라우저를 사용 하는 응용 프로그램 빌드할 수 있습니다. 않아 응용 프로그램을 지 원하는 JavaScript 브라우저와 하지 않는 브라우저를 사용 합니다.

JavaScript 지원 브라우저로 않아 응용 프로그램을 사용 하는 경우 더 나은 사용자 환경을 해야 합니다. 예를 들어 연락처 그룹을 클릭할 때 연락처를 표시 하는 페이지의 영역에만 업데이트 됩니다.

반면에 않아 응용 프로그램 브라우저가 JavaScript를 지원 하지 않는 (또는 사용 하지 않도록 설정 하는 JavaScript가) 사용 하는 경우는 약간 덜 바람직합니다 사용자 경험을 해야 합니다. 예를 들어 연락처 그룹을 클릭할 때 전체 인덱스 뷰 게시 해야 브라우저에 다시 일치 하는 연락처 목록을 표시 하기 위해 합니다.

## <a name="adding-the-required-javascript-files"></a>필요한 JavaScript 파일 추가

세 개의 JavaScript 파일을 사용 하 여 응용 프로그램에 Ajax 기능을 추가 해야 합니다. 새 ASP.NET MVC 응용 프로그램의 스크립트 폴더에 이러한 파일의 세 가지를 모두 포함 됩니다.

응용 프로그램의 여러 페이지에서 Ajax를 사용 하려는 경우 다음 편이 응용 프로그램의 뷰 마스터 페이지에 필요한 JavaScript 파일을 포함 합니다. 이런 방식으로 JavaScript 파일은 모든 응용 프로그램에서 페이지의 자동으로 포함 합니다.

다음 JavaScript 내에 포함 되어 추가 &lt;h e a d&gt; 뷰 마스터 페이지의 태그:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Ajax를 사용 하 여 인덱스 뷰를 리팩터링 합니다.

연락처를 표시 하는 보기의 영역을 업데이트만 두 번 클릭 하면 연락처 우리의 인덱스 뷰를 수정 하 여 시작 s를 사용 합니다. 그림 1에 빨간색 상자를 업데이트 하려고 하는 영역을 포함 합니다.


[![만 연락처를 업데이트합니다.](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**그림 01**: 연락처만 업데이트 ([전체 크기 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-vb/_static/image2.png))


첫 번째 단계는 별도 부분 (사용자 정의 컨트롤 보기)에 비동기적으로 업데이트 하려고 하는 보기의 일부를 분리 하는 것입니다. 연락처의 테이블을 표시 하는 인덱스 뷰 섹션 목록 1의 부분으로 이동 되었습니다.

**1-Views\Contact\ContactList.ascx 나열**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

목록 1의 부분 보다 인덱스 뷰를 다른 모델에 있는지 확인 합니다. *Inherits* 특성에 &lt;% 페이지 % @&gt; 지시문 partial는 ViewUserControl에서 상속 되도록 지정&lt;그룹&gt; 클래스입니다.

업데이트 된 인덱스 뷰 목록 2에 포함 됩니다.

**2-Views\Contact\Index.aspx 나열**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

에 대 한 업데이트 된 보기 목록 2에는 두 가지입니다. 첫째, 모든 콘텐츠는 부분으로 이동 하는 예 고 Html.RenderPartial() 호출 하 여 대체 됩니다. Html.RenderPartial() 메서드는 연락처의 초기 집합을 표시 하기 위해 인덱스 뷰를 처음 요청할 때 호출 됩니다.

둘째, 메일 그룹을 표시 하는 데는 Html.ActionLink() 통지는 Ajax.ActionLink()로 바뀌었습니다. 다음 매개 변수는 Ajax.ActionLink() 라고 합니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

첫 번째 매개 변수 링크에 대해 표시할 텍스트를 나타내는, 경로 값을 나타내는 두 번째 매개 변수 및 Ajax 옵션을 나타내는 세 번째 매개 변수입니다. 이 경우 HTML를 가리키도록 UpdateTargetId Ajax 옵션을 사용 했습니다 &lt;div&gt; Ajax 요청이 완료 된 후 업데이트에 태그입니다. 업데이트할는 &lt;div&gt; 새 연락처 목록이 포함 된 태그가 있습니다.

연락처 컨트롤러의 업데이트 된 index () 메서드 목록 3에 포함 됩니다.

**3-Controllers\ContactController.vb (인덱스 메서드)를 나열합니다.**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

조건에 따라 업데이트 된 index () 작업 다음 두 가지 중 하나를 반환 합니다. Ajax 요청에 의해 index () 작업을 호출할 경우 컨트롤러는 부분을 반환 합니다. Index () 작업, 전체 보기를 반환합니다.

Ajax 요청에 의해 호출 되 면 많은 데이터를 반환 하는 index () 동작 필요 하지 않습니다 확인 합니다. 일반 요청 컨텍스트에서 인덱스 동작 메일 그룹 및 연락처 선택한 그룹의 모든 목록을 반환합니다. Ajax 요청 컨텍스트에서 index () 동작 선택 된 그룹에만 반환합니다. Ajax는 데이터베이스 서버에 더 적은 작업을 의미합니다.

이 수정 된 인덱스 뷰 상위 및 하위 수준 모두 브라우저의 경우 작동합니다. 메일 그룹을 클릭 하면 JavaScript를 지원 하는 경우 연락처 목록을 포함 하는 보기 영역에만 업데이트 됩니다. 반면에 브라우저가 JavaScript를 지원 하지 않습니다, 경우에 전체 뷰가 업데이트 됩니다.


이 업데이트 된 인덱스 뷰에 한 가지 문제가 있습니다. 메일 그룹을 클릭할 때 선택 된 그룹 되지 강조 표시 됩니다. Ajax 요청 중에 업데이트 되는 해당 지역 외부 그룹 목록이 표시 됩니다, 때문에 올바른 그룹 강조 표시 가져올지 않습니다. 다음 섹션에서이 문제를 수정할 차례입니다.


## <a name="adding-jquery-animation-effects"></a>JQuery 애니메이션 효과 추가합니다.

일반적으로 웹 페이지의 링크를 클릭할 때 브라우저를 적극적으로 업데이트 된 콘텐츠를 페치하 여부를 검색 하려면 브라우저 진행률 표시줄을 사용할 수 있습니다. Ajax 요청을 수행할 때 반면에 브라우저 진행률 표시줄이 표시 되지 않습니다 진행 상황. 이 수 없게 사용자 우려 됩니다. 브라우저가 고정 되어 있는지 여부를 어떻게 알 수 있을까요?

작업이 Ajax 요청을 수행 하는 동안 수행 되는 사용자에 게 나타낼 수 있는 여러 가지가 있습니다. 한 가지 방법은 간단한 애니메이션을 표시 하는 것입니다. 예를 들어 Ajax 요청이 시작 되 고 요청이 완료 되는 지역에서 페이드 때 영역 아웃 페이드 수 있습니다.

애니메이션 효과를 만들 Microsoft ASP.NET MVC 프레임 워크에 포함 된 jQuery 라이브러리를 사용 합니다. 업데이트 된 인덱스 뷰 목록 4에 포함 되어 있습니다.

**4-Views\Contact\Index.aspx 나열**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

업데이트 된 인덱스 뷰 세 개의 새로운 JavaScript 함수가 포함 되어 있는지 확인 합니다. 처음 두 함수 페이드 아웃 하 여 새 메일 그룹을 클릭 하면 연락처 목록에 페이드 jQuery를 사용 합니다. 세 번째 함수에서 오류가 (예를 들어 네트워크 시간 제한) 때 Ajax 요청 결과 오류 메시지가 표시 됩니다.

또한 첫 번째 함수는 선택한 그룹을 강조 표시 담당 합니다. 클래스 = 선택한 특성은 클릭 하면 요소의 부모 요소 (LI 요소)에 추가 합니다. 다시, jQuery 쉽게 적합 한 요소를 선택 하는 CSS 클래스를 추가 합니다.

이 스크립트 그룹 연결 Ajax.ActionLink() 위해 AjaxOptions 매개 변수를 사용 하 여 연결 됩니다. 업데이트 된 Ajax.ActionLink()이 메서드는 다음과 같습니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>브라우저 기록 지원 추가

일반적으로 페이지를 업데이트 하려면 링크를 클릭 하면 브라우저 기록을 업데이트 됩니다. 이런 방식으로 페이지의 이전 상태 시간으로 다시 이동 하려면 브라우저 뒤로 단추를 클릭 수 있습니다. 예를 들어 친구 메일 그룹을 클릭 하 고 비즈니스 메일 그룹을 클릭 하는 경우 친구 연락처 그룹 선택 될 때 페이지의 상태를 다시 탐색할 브라우저 뒤로 단추를 클릭 수 있습니다.

안타깝게도, Ajax 요청을 수행 업데이트 되지 않는 브라우저 기록을 자동으로 합니다. 메일 그룹을 클릭 하 고는 Ajax 요청으로 연락처를 일치 하는 목록을 검색 하는 경우 브라우저 기록을 업데이트 되지 않습니다. 새 메일 그룹을 선택한 후 메일 그룹으로 다시 이동 하는 브라우저 뒤로 단추를 사용할 수 없습니다.

하려는 경우 사용자가 브라우저를 다시 사용할 수 있도록 단추 Ajax 요청을 수행한 후 좀 더 많은 작업을 수행 해야 합니다. ASP.NET AJAX 프레임 워크에 기본 제공 브라우저 기록 관리 기능을 사용 해야 합니다.

ASP.NET AJAX 브라우저 기록을 다음 세 가지 작업을 수행 해야 했습니다.

1. 브라우저 기록 enableBrowserHistory 속성을 true로 설정 하 여 사용 합니다.
2. AddHistoryPoint() 메서드를 호출 하 여 보기의 상태가 변경 될 때 기록 점을 저장 합니다.
3. 탐색 이벤트가 발생할 때 보기의 상태를 다시 구성 합니다.

업데이트 된 인덱스 뷰 목록 5에 포함 됩니다.

**5-Views\Contact\Index.aspx 나열**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

목록 5에서 브라우저 기록은 pageInit() 함수에서 사용 됩니다. PageInit() 함수는 탐색 이벤트에 대 한 이벤트 처리기를 설정도 사용 됩니다. 브라우저 앞으로 또는 뒤로 단추 변경 하려면 페이지의 상태를 발생 시킬 때마다 navigate 이벤트가 발생 합니다.

BeginContactList() 메서드는 메일 그룹을 클릭할 때 호출 됩니다. 이 메서드는 새 기록 점을 addHistoryPoint() 메서드를 호출 하 여 만듭니다. 클릭 하면 연락처 그룹의 id 기록에 추가 됩니다.

그룹 id의 메일 그룹 링크에 대 한 expando 특성에서 검색 됩니다. 링크는 다음 호출 Ajax.ActionLink()로 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

마지막 매개 변수는 Ajax.ActionLink()에 전달 된 groupid (XHTML 호환성을 위해 소문자) 링크에 expando 특성을 추가 합니다.

사용자는 브라우저 뒤로 또는 앞으로 단추에 도달 하는 경우 탐색 이벤트가 발생 하 고 navigate() 메서드를 호출 합니다. 이 메서드는 탐색 메서드에 전달 된 브라우저 기록 점을에 해당 하는 페이지의 상태와 일치 하도록 페이지에 표시 된 연락처를 업데이트 합니다.

## <a name="performing-ajax-deletes"></a>Ajax 수행 삭제

현재 연락처를 삭제 해야 삭제 링크를 클릭 하 고 삭제 확인 페이지에 표시 된 삭제 단추를 클릭 한 다음 (그림 2 참조). 이 작업을 수행할 데이터베이스 레코드를 삭제와 같은 간단한 페이지 요청을 많이 처럼 보입니다.


[![삭제 확인 페이지](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**그림 02**: 삭제 확인 페이지 ([전체 크기 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-vb/_static/image4.png))


삭제 확인 페이지를 건너뛰고 인덱스 뷰에서 직접 연락처를 삭제 하기 쉽습니다. 이 접근 방식을 사용할 경우 보안 허점이에 응용 프로그램을 열기 때문에이 유혹을 피해 야 합니다. 일반적으로 don t 웹 응용 프로그램의 상태를 수정 하는 작업을 호출할 때 HTTP GET 작업을 수행 하려고 합니다. Delete를 수행 하는 경우 HTTP POST를 수행 하거나, HTTP DELETE 작업 하려는 합니다.

링크가 삭제 부분 ContactList에 포함 됩니다. 업데이트 된 버전의 부분 ContactList 목록 6에 포함 됩니다.

**6-Views\Contact\ContactList.ascx 나열**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

링크가 삭제 Ajax.ImageActionLink() 메서드 호출으로 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink() ASP.NET MVC 프레임 워크의 표준 일부가 아닙니다. Ajax.ImageActionLink() 않아 프로젝트에 포함 된 사용자 지정 도우미 메서드는입니다.


위해 AjaxOptions 매개 변수는 다음과 같은 두 가지 속성이 있습니다. 첫째, Confirm 속성 팝업 JavaScript 확인 대화 상자를 표시 하려면 사용 됩니다. 둘째, HttpMethod 속성은 HTTP DELETE 작업 수행 하기 위해 사용 됩니다.

목록 7 연락처 컨트롤러에 추가 된 새 AjaxDelete() 동작을 포함 합니다.

**7-Controllers\ContactController.vb (AjaxDelete)를 나열합니다.**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete() 작업 AcceptVerbs 특성으로 데코레이팅되 어 있습니다. 이 특성에는 HTTP DELETE 작업 외의 HTTP 작업에서 제외 하 고 호출 될 작업이 하지 않도록 합니다. 특히,이 작업을 HTTP GET을 호출할 수 없습니다.

데이터베이스 레코드를 삭제 한 후 삭제 된 레코드를 포함 하지 않는 업데이트 된 연락처 목록을 표시 해야 합니다. AjaxDelete() 메서드 부분 ContactList 및 업데이트 된 연락처 목록을 반환합니다.

## <a name="summary"></a>요약

이 반복에 않아 응용 프로그램에 Ajax 기능을 추가 했습니다. 응답성 및 응용 프로그램의 성능을 개선 하기 위해 Ajax를 사용 했습니다.

첫째, 두 번 클릭 하면 연락처 전체 보기는 업데이트 되지 않는 인덱스 뷰를 리팩터링 했습니다. 대신, 연락처 목록을 업데이트만 연락처 그룹을 클릭 합니다.

다음으로, jQuery 애니메이션 효과를 페이드 아웃 페이드 인 연락처 목록을 사용 했습니다. Ajax 응용 프로그램에 애니메이션 추가 데 사용할 수는 브라우저 진행률 표시줄을 해당 하는 응용 프로그램의 사용자에 게 제공 합니다.

또한 Ajax 응용 프로그램을 브라우저 기록 지원이 추가 되었습니다. 에서는 사용자가 브라우저를 다시 클릭 하 고 앞으로 인덱스 뷰 상태를 변경 하는 단추를 사용할 수 있습니다.

마지막으로, HTTP DELETE 작업을 지 원하는 삭제 링크를 만들었는지 여부입니다. Ajax 삭제를 수행 하 여 사용자를 추가 삭제 확인 페이지를 요청 하지 않고도 데이터베이스 레코드를 삭제 하려면 사용자가 설정 합니다.

>[!div class="step-by-step"]
[이전](iteration-6-use-test-driven-development-vb.md)
