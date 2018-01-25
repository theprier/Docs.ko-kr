---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: "폼 인증 구성 및 고급 항목 (VB) | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 다양 한 폼 인증 설정을 검사 하 고 폼 요소를 통해 수정 하는 방법을 참조 합니다. 이것을 통해 설명을 수반 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/14/2008
ms.topic: article
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: fe4c421f248e325b69be7cad6c10bcbedf59ae5f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="forms-authentication-configuration-and-advanced-topics-vb"></a>폼 인증 구성 및 고급 항목 (VB)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> 이 자습서에서는 다양 한 폼 인증 설정을 검사 하 고 폼 요소를 통해 수정 하는 방법을 참조 합니다. 이 작업을 사용자 지정 URL (예: SignIn.aspx Login.aspx 대신)와 cookieless 폼 인증 티켓 로그인 페이지를 사용 하 여 폼 인증 티켓 시간 제한 값을 사용자 지정에 대해 자세히를 수반 됩니다.


## <a name="introduction"></a>소개

에 [이전 자습서](an-overview-of-forms-authentication-vb.md) 로그인 페이지를 표시 하려면 다른 만들지를 Web.config에서 구성 설정을 지정 하에서 ASP.NET 응용 프로그램에서 폼 인증을 구현 하는 데 필요한 단계에서 인증 되 고 익명 사용자에 대 한 내용입니다. 모드 특성을 설정 하 여 폼 인증을 사용 하도록 웹 사이트를 구성 했습니다 회수는 &lt;인증&gt; 요소 폼에 적용 합니다. &lt;인증&gt; 요소 포함 되기도 &lt;forms&gt; 자식 요소에는 다양 한 폼 인증 설정을 지정할 수 있습니다.

이 자습서에서는 다양 한 폼 인증 설정을 검사 하 고 사용 하 여 수정 하는 방법을 참조 합니다는 &lt;forms&gt; 요소입니다. 이 작업을 사용자 지정 URL (예: SignIn.aspx Login.aspx 대신)와 cookieless 폼 인증 티켓 로그인 페이지를 사용 하 여 폼 인증 티켓 시간 제한 값을 사용자 지정에 대해 자세히를 수반 됩니다. 또한 폼 인증 티켓의 구성을 더 자세히 검사 하 고 ASP.NET 티켓의 데이터를 검사 하 고 변조에서 안전 하는 데 걸리는 예방 조치를 참조 합니다. 마지막으로 폼 인증 티켓에 추가 되는 사용자 데이터를 저장 하는 방법과 사용자 지정 보안 주체 개체를 통해이 데이터를 모델링 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>1 단계: 검사 하는 &lt;forms&gt; 구성 설정

Asp.net에서 폼 인증 시스템에서는 다양 한 응용 프로그램에서 응용 프로그램 별로 사용자 지정할 수 있는 구성 설정 제공 합니다. 여기에 같은 설정이 포함: 수명의 폼 인증 티켓입니다. 어떤 종류의 보호 티켓;에 적용 됩니까 티켓은 어떤 조건 쿠키 인증에서 사용 됩니다. 로그인 페이지;의 경로를 및 기타 정보입니다. 기본값을 수정 하려면 추가 [ &lt;forms&gt; 요소](https://msdn.microsoft.com/library/1d3t3c61.aspx) 의 자식으로는 [ &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx), 해당 속성을 지정 XML 특성으로 사용자 지정 하려면 값 같은 됩니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

표 1에는 통해 지정할 수 있는 속성이 요약 되어 있습니다.는 &lt;forms&gt; 요소입니다. Web.config는 XML 파일 이므로 왼쪽된 열에 특성 이름이 대/소문자 구분 됩니다.

| **특성** | **설명** |
| --- | --- |
| cookieless | 이 특성 지정 어떤 조건에서 인증 티켓 및 URL에 포함 되는 쿠키에 저장 됩니다. 허용 가능한 값은: UseCookies; UseUri; 자동으로 검색 합니다. 및 UseDeviceProfile (기본값)입니다. 2 단계는이 설정을 자세히 검사합니다. |
| defaultUrl | URL 쿼리 문자열에 지정 된 RedirectUrl 값이 없는 경우에 로그인 페이지에서 로그인 한 후 사용자는 리디렉션됩니다을 나타냅니다. 기본값은 default.aspx 합니다. |
| 도메인 | 쿠키 기반 인증 티켓을 사용할 경우이 설정은 쿠키의 도메인 값을 지정 합니다. 기본값은 빈 문자열입니다 (예: www.yourdomain.com) 발급 도메인을 사용 하도록 브라우저. 이 경우 쿠키를 **하지** admin.yourdomain.com 같은 하위 도메인을 요청 하면 보낼 수 있습니다. 모든 하위 도메인에 전달할 쿠키를 원하는 경우, 도메인 속성 설정 yourdomain.com을 사용자 지정 해야 합니다. |
| enableCrossAppRedirects | 동일한 서버의 다른 웹 응용 프로그램의 Url로 리디렉션할 때 인증 된 사용자가 저장 하는지 여부를 나타내는 부울 값입니다. 기본값은 false입니다. |
| loginUrl | 로그인 페이지의 URL입니다. 기본값은 login.aspx입니다. |
| name | 쿠키의 이름, 쿠키 기반 인증 티켓을 사용할 때 기본값은입니다. ASPXAUTH 합니다. |
| path | 쿠키 기반 인증 티켓을 사용할 경우이 설정은의 쿠키 경로 특성을 지정 합니다. Path 특성에는 개발자를 특정 디렉터리 계층 구조를 쿠키의 범위를 제한할 수 있습니다. 기본값은 / 도메인에 대 한 모든 요청을 인증 티켓 쿠키를 보낼 브라우저에 게 알립니다. |
| 보호 | 폼 인증 티켓을 보호 하기 위해 어떤 기술을 사용을 나타냅니다. 허용 가능한 값은: 모두 (기본값); 암호화; 해당 항목이 없습니다. 및 유효성 검사 합니다. 이러한 설정에 대해서는 3 단계에서에서 자세히 설명 합니다. |
| requireSSL | 인증 쿠키를 전송 하는 SSL 연결이 필요한 지 여부를 나타내는 부울 값입니다. 기본값은 false입니다. |
| slidingExpiration | 사용자가 단일 세션에서 사이트를 방문할 인증 쿠키 s 시간 초과 될 때마다 다시 설정 하는지 여부를 나타내는 부울 값입니다. 기본값은 true입니다. 인증 티켓 시간 제한 정책에는 지정 하면 보다 자세히 설명 되어 티켓 시간 제한 값 섹션 s입니다. |
| 시간 제한 | 인증 티켓 쿠키가 만료 된 후 분 후에는 시간을 지정 합니다. 기본값은 30입니다. 인증 티켓 시간 제한 정책에는 지정 하면 보다 자세히 설명 되어 티켓 시간 제한 값 섹션 s입니다. |

**표 1**: A 요약은 &lt;forms&gt; 요소의 특성

ASP.NET 2.0 이상, 기본 폼 인증 값 FormsAuthenticationConfiguration 클래스는.NET Framework에서 하드 코드 되어 있습니다. 모든 수정 Web.config 파일에서 응용 프로그램에서 응용 프로그램 별로 적용 되어야 합니다. ASP.NET이 점에서 차이가 1.x, 여기서 폼 인증 기본값 machine.config 파일에 저장 된 (및 따라서 machine.config를 편집을 통해 수정할 수 있습니다). ASP.NET의 주제 시 1.x는 것이 좋은지를 언급 하기 위해 다양 한 폼 인증 시스템 설정 ASP.NET 2.0에서 다양 한 기본 값을 갖도록 및 ASP.NET에서 보다 그 이상 1.x 합니다. ASP.NET 1.x 환경에서 응용 프로그램을 마이그레이션하려는 경우에 이러한 차이에 주의 해야 합니다. 참조 [는 &lt;forms&gt; 요소 기술 문서](https://msdn.microsoft.com/library/1d3t3c61.aspx) 차이점 목록에 대 한 합니다.

> [!NOTE]
> 결과 폼 인증 티켓 쿠키에 대 한 세부 정보를 지정 하는 시간 제한, 도메인 및 경로 같은 여러 폼 인증 설정. 에 대 한 자세한 내용은 쿠키, 작동 방법 및 다양 한 속성을 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)합니다.


### <a name="specifying-the-tickets-timeout-value"></a>티켓의 시간 제한 값 지정

폼 인증 티켓에는 id를 나타내는 토큰입니다. 쿠키 기반 인증 티켓으로이 토큰은 쿠키의 형태로 유지 되 고 각 요청에 대해 웹 서버로 전송 합니다. 토큰 소유 여부는 사실, 선언, 저는 *username*에 이미 로그인 한 했으며 방문 페이지에서 사용자의 id를 기억할 수 있도록 사용 됩니다.

폼 인증 티켓 사용자의 id를 포함 합니다. 뿐만 아니라도 무결성 및 보안 토큰의 유용한 정보를 포함 합니다. 즉, 돌파 유효한 토큰 underhanded 어떤 방식으로든에서 수정 하거나 불법 토큰을 만들 수 원하는 하지 않습니다.

티켓에 포함 되는 정보의 이러한 1 비트는는 *만료*, 이것은 날짜 및 시간 티켓은 더 이상 유효 합니다. 인증 티켓을 검사 하는 FormsAuthenticationModule 때마다 티켓의 만료 아직 전달 되지 않은 되도록 합니다. 있는 경우, 티켓을 무시 하 고 익명으로 사용자를 식별 합니다. 이러한 안전 장치는 재생 공격 으로부터 보호 합니다. 해커가 자신의 컴퓨터에 대 한 실제 액세스를 확보 하 고 해당 쿠키를 통해 루 팅 여 아마도 그녀의 관련 한 실질적인-사용자의 유효한 인증 티켓을 가져올 수-이 훔친된 인증 티켓을 사용 하 여 서버에는 요청을 보낼 수 있습니다 하는 경우에 만료 없이 및 항목을 수 있습니다. 만료가이 시나리오를 방지 하지 않는 동안는 이러한 공격 성공할 수 있는 창을 제한 합니다.

> [!NOTE]
> 폼 인증 시스템에서 인증 티켓을 보호 하기 위해 사용 하는 세부 정보 추가 기술의 3 단계.


인증 티켓을 만들 때 폼 인증 시스템의 만료 시간 제한 설정을 참조 하 여 결정 합니다. 표 1, 설정이 기본적으로 30 분 시간 제한에서에서 설명한 것 처럼 폼 인증 티켓 만들어질 때의 만료 날짜 및 시간 앞으로 30 분으로 설정 한다는 의미입니다.

만료 된 절대 시간 앞으로 폼 인증 티켓 만료 될 때를 정의 합니다. 하지만 일반적으로 개발자는 사용자는 사이트 다시 검토 하 여 될 때마다 다시 설정 하는 슬라이딩 만료를 구현 합니다. 이 동작은 slidingexpiration이 설정에 따라 결정 됩니다. 경우 true로 설정 (기본값) 이면 사용자를 인증 하는 FormsAuthenticationModule 될 때마다 업데이트 티켓의 만료 합니다. 각 요청에 대해 업데이트 되지 않습니다 만료 false로 설정 하는 경우 티켓을 티켓 처음 경과 된 분 수 정확 하 게 제한 시간 만료로 인해 생성 됩니다.

> [!NOTE]
> 인증 티켓에 저장 된 만료 절대 날짜 및 시간 값을 2008 년 8 월 2 일 오전 11시 34분 같은 됩니다. 또한, 날짜 및 시간 웹 서버의 현지 시간 기준 으로합니다. 이 디자인 결정에 따라 몇 가지 흥미로운 부작용 주위 일광 절약 시간제 DST (), United States의 시계를 이동할 때 계속 1 시간 (웹 서버는 일광 절약 시간제 관찰 되는 로캘에서 호스팅되는 경우)이 있을 수 있습니다. 근처 DST 시작 되는 시간 30 분 만료 된 ASP.NET 웹 사이트에 대 한 어떻게 될 지는 것이 좋습니다 (않는 오전 2 시에). 방문자가 사이트에 로그온 2008 년 3 월 11 일 오전 1 시 55 가정해 보세요. 이 오전 2 시 25 (30 분에 나중에 해당) 2008 년 3 월 11 일에 만료 되는 폼 인증 티켓을 생성 합니다. 그러나 오전 2시 시점이, 클록 처리기로 이동 오전 3시 DST 때문입니다. 사용자 (오전 3시 01분)에서 로그인 한 후 6 분 후 새 페이지를 로드 하는 경우 티켓 만료 되 고 사용자의 로그인 페이지를 리디렉션합니다.는 FormsAuthenticationModule 인식 합니다. Stefan Schackow의 복사본을 선택에 대 한 보다 철저 한 내용은이 및 다른 인증 티켓 시간 제한 의문 사항을으로 해결 방법, *Professional ASP.NET 2.0 보안, 구성원 자격 및 역할 관리* (ISBN: 978-0-7645-9698-8).


그림 1 slidingexpiration이 false로 설정 되 고 시간 제한은 30으로 설정 하는 경우 워크플로 보여 줍니다. 로그인 할 때 생성 된 인증 티켓이 만료 날짜를 포함 하 고 이후 요청에서이 값은 업데이트 되지 않습니다. FormsAuthenticationModule 티켓이 만료 되었습니다을 발견할 경우을 무시 하 고 익명으로 요청을 처리 합니다.


[![그래픽으로 폼 인증 티켓 만료 때 slidingExpiration이 false](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**그림 01**: A 그래픽으로 폼 인증 티켓 만료 때 slidingExpiration이 false ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png))


그림 2 slidingExpiration로 설정 된 경우 워크플로가 나와 true 및 제한 시간 30으로 설정 됩니다. (만료 되지 않은 티켓)으로 인증 된 요청을 받으면 해당 만료 시간 (분) 이후에 시간 초과 수로 업데이트 됩니다.


[![폼 인증 티켓의 그래픽 표현을 slidingExpiration 중 하면](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**그림 02**: 폼 인증 티켓의 그래픽 표현을 A slidingExpiration가 true ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png))


쿠키 기반 인증 티켓 (기본값)를 사용할 때이 토론 쿠키 지정 자신의 expiries 있을 수도 있습니다 때문에 다소 혼동 됩니다. 쿠키의 만료 (또는 결핍) 쿠키를 제거 해야 하는 경우 브라우저에 지시 합니다. 쿠키가 없는 경우 expiry, 브라우저 종료 될 때 소멸 되기 합니다. 그러나 만료가 있는 경우 날짜까지 쿠키는 사용자의 컴퓨터에 저장 및 만료에 지정 된 시간이 지나면 합니다. 브라우저에서 쿠키 소멸 될 때 더 이상 웹 서버에 전송 됩니다. 따라서 쿠키의 소멸은 사용자 사이트에서 로깅 비슷합니다.

> [!NOTE]
> 물론, 사용자의 컴퓨터에 저장 된 쿠키를 적극적으로 제거할 수 있습니다. Internet Explorer 7, 도구, 옵션로 이동 하 고 탐색 기록 구역에서 삭제 단추를 클릭 합니다. 여기에서 삭제 쿠키 단추를 클릭 합니다.


폼 인증 시스템에 전달 되는 값에 따라 세션 또는 만료 기반 쿠키를 만듭니다는 *persistCookie* 매개 변수입니다. 두 입력된 매개 변수에서 FormsAuthentication 클래스 GetAuthCookie, SetAuthCookie, 및 RedirectFromLoginPage 메서드를 사용 하는 회수: *username* 및 *persistCookie*합니다. 이전 자습서에서 만든 로그인 페이지 포함 암호 저장 CheckBox 영구 쿠키 생성 되는지 여부를 결정 합니다. 영구 쿠키는 만료부터 시작 합니다. 비 영구적인 쿠키는 세션 기반입니다.

앞에서 설명한 제한 시간 및 slidingExpiration 개념 두 세션 및 만료 기반 쿠키에 동일 하 게 적용 합니다. 실행에 사소한 차이점이 하나만: true로 설정 된 slidingTimeout 함께 만료 기반 쿠키를 사용 하면 쿠키의 만료만 업데이트 됩니다 경과 된 시간 중 절반 이상.

슬라이딩 만료를 사용 하 여 제한 시간 (60 분)을 1 시간 후 티켓을 할당 하는 웹 사이트의 인증 티켓 시간 제한 정책 업데이트 하겠습니다. 이 변경 내용을 적용, Web.config 파일을 업데이트 하려면 추가 &lt;forms&gt; 요소에는 &lt;인증&gt; 요소를 다음 태그로:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Login.aspx 이외의 로그인 페이지 URL을 사용 하 여

FormsAuthenticationModule 권한이 없는 사용자가 로그인 페이지로 자동으로 리디렉션합니다, 이후 로그인 페이지의 URL을 알고 있어야 합니다. 이 URL에서 로그인 Url 특성에 지정 된는 &lt;forms&gt; 요소 및 기본값은 login.aspx입니다. 기존 웹 사이트를 통해 이식 하는 경우 이미 책갈피가 설정 및 검색 엔진 있는 다른 URL로 로그인 페이지를 이미 있을 수도 있습니다. 기존 로그인 페이지를 login.aspx 이름 바꾸기 링크와 사용자의 책갈피를 분리 하는 대신 로그인 페이지를 가리키도록 loginUrl 특성 대신 수정할 수 있습니다.

예를 들어 로그인 페이지 SignIn.aspx 변수의 이름이 사용자 디렉터리에 있는 경우 로그인 Url 구성 설정 ~/Users/SignIn.aspx 가리킬 수 같이:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

없기 때문에 이미 현재 응용 프로그램에 Login.aspx 라는 로그인 페이지에 사용자 지정 값을 지정할 필요가 없습니다는 &lt;forms&gt; 요소입니다.

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>Cookieless 폼 인증 티켓을 사용 하 여 2 단계:

기본적으로 폼 인증 시스템 쿠키 컬렉션에 해당 인증 티켓을 저장 하거나 사이트를 방문 하는 사용자 에이전트에 따라 URL에 포함 여부를 결정 합니다. 기본 지원 데스크톱 브라우저의 경우 모든 Internet Explorer, Firefox, Opera, 및 Safari, 지원 쿠키 비슷하지만 되지 모든 모바일 장치 않습니다.

폼 인증 시스템에서 사용 하는 쿠키 정책이의 쿠키 설정에 따라는 &lt;forms&gt; 요소를 지정할 수 있는 4 개의 값 중 하나:

- UseCookies-쿠키 기반 인증 티켓 항상 사용될지를 지정 합니다.
- UseUri-쿠키 기반 인증 티켓 사용 되지 않습니다 나타냅니다.
- 자동 검색-장치 프로필 쿠키, 쿠키 기반 인증 티켓을 지원 하지 않는 경우 사용 되지 않습니다. 장치 프로필에서 쿠키를 지 원하는 경우 쿠키는 사용할 수 있는지 확인 하는 프로브 메커니즘 사용 됩니다.
- UseDeviceProfile-기본; 장치 프로필에서 쿠키를 지원 하는 경우에 쿠키 기반 인증 티켓을 사용 합니다. 검색 메커니즘이 사용 됩니다.

자동 검색 및 UseDeviceProfile 설정을 의존는 *장치 프로필* 쿠키 기반 또는 쿠키 인증 티켓을 사용할 것인지를 구축 방향을 얻기 위한에서. ASP.NET에는 다양 한 장치와 기능, 쿠키를 지원 하는지 여부, 버전을 지 원하는 JavaScript 등과 같은 데이터베이스 유지 관리 합니다. 될 때마다 장치에서 웹 페이지를 따라 보내는 웹 서버에서 요청 된 *사용자 에이전트* 장치 유형을 식별 하는 HTTP 헤더입니다. ASP.NET 해당 프로필이 해당 데이터베이스에 제공 된 사용자 에이전트 문자열을 자동으로 일치 합니다.

> [!NOTE]
> 이 데이터베이스의 장치 기능을 준수 하는 여러 개의 XML 파일에에서 저장 됩니다는 [브라우저 정의 파일 스키마](https://msdn.microsoft.com/library/ms228122.aspx)합니다. 기본 장치 프로필 파일 %WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers에서 있습니다. 응용 프로그램의 응용 프로그램에 사용자 지정 파일을 추가할 수도 있습니다\_브라우저 폴더입니다. 자세한 내용은 참조 [방법: ASP.NET 웹 페이지에서 브라우저 종류를 검색](https://msdn.microsoft.com/library/3yekbd5b.aspx)합니다.


기본 설정은 UseDeviceProfile 이기 때문에 쿠키가 없는 폼 인증 티켓 장치 프로필이 쿠키를 지원 하지 않으면 보고 사이트를 방문 하는 경우 사용 됩니다.

### <a name="encoding-the-authentication-ticket-in-the-url"></a>URL에서 인증 티켓 인코딩

쿠키는 브라우저에서 정보를 포함 하 여 기본 폼 인증 설정 방문 장치가 지 원하는 경우 쿠키를 사용 하는 이유는 특정 웹 사이트에 각 요청에 대 한 자연 보통입니다. 쿠키 지원 되지 않는 경우 서버에 클라이언트에서 인증 티켓을 전달 하기 위한 방법 채택 해야 합니다. 쿠키가 없는 환경에서 사용 되는 일반적인 해결 방법은 URL에 쿠키 데이터를 인코딩하려면 되려고 합니다.

URL 내의 등의 정보가 포함 될 수 있습니다 어떻게 볼 수 없는 인증 티켓을 사용 하도록 사이트를 강제로 가장 좋은 방법은 합니다. UseUri cookieless 구성 설정을 설정 하 여이 수행할 수 있습니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

이 변경 내용을 적용 하 고 나면 브라우저를 통해 사이트를 방문 합니다. 익명 사용자로 방문 하면 Url 전과 정확히 일치 보입니다. 예를 들어 Default.aspx 페이지를 방문 하는 경우 내 브라우저의 주소 표시줄에 다음 URL 보여 줍니다.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

그러나 로그인 시 폼 인증 티켓 URL에 포함 됩니다. 예를 들어 로그인 페이지를 방문 하 고 Sam로 로그인 후 Default.aspx 페이지에 반환 되 고 I 있지만 URL이 시간은:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

URL 내에서 폼 인증 티켓에 포함 된 합니다. 문자열 (F (jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv rfezq0gKadKX0YPZCkA2) 쿠키 내에서 주로 저장 되는 동일한 데이터 이며 16 진수로 인코딩된 인증 티켓 정보를 나타냅니다.

작동 하도록 쿠키 인증 티켓을 위해 시스템에 인증 티켓 데이터를 포함 하는 페이지에 있는 모든 Url 인코딩해야 합니다., 그렇지 않으면 인증 티켓 것입니다 손실 링크를 클릭할 때입니다. 다행히도 포함이 논리는 자동으로 수행 됩니다. 이 기능을 보여 주기 위해 Default.aspx 페이지를 열고 테스트 연결 및 SomePage.aspx, 텍스트 및 NavigateUrl 속성을 각각 설정 하이퍼링크 컨트롤을 추가 합니다. 실제로 아님을 페이지 SomePage.aspx 라는 프로젝트에 문제가 되지 않습니다.

Default.aspx의 변경 내용을 저장 한 후 브라우저를 통해 방문 하는 것입니다. 폼 인증 티켓 URL에 포함 하는 사이트에 로그온 합니다. 그런 다음 Default.aspx를에서 링크 테스트 링크를 클릭 합니다. 어떻게 된 것입니까? SomePage.aspx 라는 페이지가 없는 경우 404 오류 발생 후 수 있지만 것이 아니라 중요 한 여기. 대신, 브라우저의 주소 표시줄에 집중 합니다. URL에서 폼 인증 티켓을 포함 하는 참고!

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

링크의 URL SomePage.aspx 인증 티켓-를 포함 하는 URL에 자동으로 변환 필요는 전혀 없고 코드가 전혀 작성! Http://로 시작 하는 모든 하이퍼링크에 대 한 URL에 자동으로 포함 될 폼 인증 티켓 또는 /. Response.Redirect에 대 한 호출, 하이퍼링크 컨트롤 또는 HTML 앵커 요소 하이퍼링크가 표시 되 면 문제가 되지 않습니다 (즉, &lt;는 href = "..."&gt;... &lt;/a&gt;). URL 예 http://www.someserver.com/SomePage.aspx 또는 /SomePage.aspx 아닌,으로 폼 인증 티켓을 수행해 줍니다 포함 됩니다.

> [!NOTE]
> Cookieless 폼 인증 티켓을 동일한 쿠키 기반 인증 티켓 시간 제한 정책을 준수합니다. 그러나 쿠키 인증 티켓은 URL에서 직접 인증 티켓이 포함 되어 있으므로 재생 공격 가능성이 더 큽니다. 사용자가 웹 사이트를 방문 하 고, 로그인 동료에 게 전자 메일에 URL을 붙여 다음 가정해 보세요. 동료는 만료에 도달 하기 전에 해당 링크를 클릭, 하는 경우 이러한로 기록 됩니다 전자 메일을 보낸 사용자에 게!


## <a name="step-3-securing-the-authentication-ticket"></a>3 단계: 보안 인증 티켓을 설정합니다.

폼 인증 티켓은 네트워크를 통해 전송 되 쿠키에 하나 또는 URL 내에 직접 포함 합니다. Id 정보 외에도 인증 티켓이 포함 될 수 있습니다 사용자 데이터 (4 단계에서에서 알 수)입니다. 따라서 중요 한 티켓의 데이터는 암호화는 침입자 및 (중요) 하는 폼 인증 시스템 티켓으로 손상 되지 않았음을 보장할 수 있습니다.

티켓의 데이터의 개인 정보 보호를 보장 하려면 폼 인증 시스템에서 티켓 데이터를 암호화할 수 있습니다. 티켓 데이터를 암호화를 일반 텍스트로 네트워크를 통해 잠재적으로 중요 한 정보를 보냅니다.

폼 인증 시스템 해야 티켓의 신뢰성을 보장 하려면 *유효성을 검사* 티켓입니다. 유효성 검사는 데이터의 특정 부분 수정 되지 않은 하 고이 통해 수행 하는 작업을  *[메시지 인증 코드 (MAC)](http://en.wikipedia.org/wiki/Message_authentication_code)*합니다. 간단히 말해서 MAC은 작은 부분에 (이 경우 티켓) 유효성을 검사 해야 하는 데이터를 식별 하는 정보입니다. MAC에서 나타내는 데이터 수정 되 면 다음 MAC 및 데이터는 일치 하지 않습니다. 또한 계산을 통해 데이터를 수정 하 고 수정된 된 데이터와 일치 하도록 자신의 MAC 생성 해커가 하드도 합니다.

만드는 (또는 수정 하 고) 하는 경우 티켓을 폼 인증 시스템 MAC 만들고 티켓의 데이터에 연결 합니다. 후속 요청이 도착 하면 폼 인증 시스템에서 티켓 데이터의 신뢰성을 확인할 MAC 및 티켓 데이터를 비교 합니다. 그림 3이이 워크플로 그래픽으로 보여 줍니다.


[![MAC을 통해 티켓의 신뢰성은 보장](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**그림 03**: The 티켓의 신뢰성은 MAC를 통해 보장 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png))


보호 설정에 따라 어떤 보안 조치 인증 티켓에 적용 되는 &lt;forms&gt; 요소입니다. 다음 세 가지 값 중 하나에서 보호 설정을 할당 될 수 있습니다.

- 모든-티켓 모두 암호화 및 디지털 서명 않았습니다 (기본값).
- 암호화-암호화만 적용 되-없습니다 MAC이 생성 됩니다.
- None-티켓은 암호화 되거나 되지 디지털 서명 합니다.
- 유효성 검사-MAC를 생성할 수 있지만 티켓 데이터를 일반 텍스트로 네트워크를 통해 전송 됩니다.

모든 설정을 사용 하는 것이 좋습니다.

### <a name="setting-the-validation-and-decryption-keys"></a>유효성 검사 및 암호 해독 키를 설정합니다.

암호화 및 해시를 암호화 하 여 인증 티켓의 유효성을 검사 폼 인증 시스템에서 사용 하는 알고리즘은을 통해 사용자 지정할 수는 [ &lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx) Web.config에 있습니다. 표 2 윤곽선은 &lt;machineKey&gt; 요소의 특성 및 가능한 값입니다.

| **특성** | **설명** |
| --- | --- |
| 해독 | 암호화에 사용 되는 알고리즘을 나타냅니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다.-자동-기본; decryptionKey 특성의 길이에 따라 알고리즘을 결정 합니다. -AES-사용 하 여는 [표준 AES (고급 암호화)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 알고리즘입니다. -DES를 사용 하는 [표준 DES (데이터 암호화)](http://en.wikipedia.org/wiki/Data_Encryption_Standard) 이 알고리즘 계산 강력 하지 않은 것으로 간주 됩니다 하 고 사용할 수 없습니다. -3DES-사용 하 여는 [Triple DES](http://en.wikipedia.org/wiki/Triple_DES) 알고리즘을 세 번 DES 알고리즘을 적용 하 여 작동 합니다. |
| decryptionKey | 암호화 알고리즘에서 사용 하는 비밀 키입니다. 이 값 이어야 합니다. (암호 해독의 값에 기반) 적절 한 길이, AutoGenerate, 또는 두 값 중 하나를 함께 추가의 16 진수 문자열 IsolateApps 합니다. 각 응용 프로그램에 대 한 고유 값을 사용 하도록 ASP.NET에 지시 IsolateApps를 추가 합니다. 기본값은 AutoGenerate, IsolateApps 합니다. |
| 유효성 검사 | 유효성 검사에 사용 되는 알고리즘을 나타냅니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다.-AES-암호화 표준 AES (고급) 알고리즘을 사용 합니다. -M d 5-사용 하 여는 [Message-digest MD5 (5)](http://en.wikipedia.org/wiki/MD5) 알고리즘입니다. -S h a 1-사용 하 여는 [SHA1](http://en.wikipedia.org/wiki/Sha1) 알고리즘 (기본값). -3DES-Triple DES 알고리즘을 사용 합니다. |
| validationKey | 유효성 검사 알고리즘에서 사용 하는 비밀 키입니다. 이 값 이어야 합니다 (유효성 검사에 대 한 값에 기반) 적절 한 길이, AutoGenerate, 또는 두 값 중 하나를 함께 추가의 16 진수 문자열 IsolateApps 합니다. 각 응용 프로그램에 대 한 고유 값을 사용 하도록 ASP.NET에 지시 IsolateApps를 추가 합니다. 기본값은 AutoGenerate, IsolateApps 합니다. |

**표 2**:는 &lt;machineKey&gt; 요소 특성

다양 한 알고리즘의 장단점 이러한 암호화 및 유효성 검사 옵션 및 전문가 대 한 자세한 설명은이 자습서의 범위를 벗어납니다. 심층 분석 확인을 사용 하려면 어떤 암호화 및 유효성 검사 알고리즘에 대 한 지침을 포함 하 여 이러한 문제를 사용 하려면 어떤 키 길이 대 한 참조, 이러한 키를 생성 하는 최선의 방법 및 *Professional ASP.NET 2.0 보안, 구성원 자격 및 역할 관리* .

기본적으로 암호화 및 유효성 검사에 사용 되는 키 각 응용 프로그램에 대 한 자동으로 생성 되 고 이러한 키에는 로컬 보안 기관 (LSA)에 저장 됩니다. 즉, 기본 설정을 웹 서버-웹 서버와 응용 프로그램에서 응용 프로그램 별로에 고유 키를 보장 합니다. 따라서 이러한 기본 동작은 두 다음과 같은 시나리오에서 작동 하지 않습니다.

- **웹 팜** -는 [웹 팜](http://en.wikipedia.org/wiki/Web_farm) 시나리오에서는 단일 웹 응용 프로그램 확장성 및 중복성의 목적을 위해 여러 웹 서버에서 호스팅됩니다. 들어오는 각 요청은 사용자 세션의 수명 주기 동안 서로 다른 서버 있습니다 사용할 수 그의 다양 한 요청을 처리 하는 팜의 서버에 전달 됩니다. 따라서 각 서버는 폼 인증 티켓 만들어지도록 동일한 암호화 및 유효성 검사 키를 사용 해야에서 유효성을 검사 하 여 암호화를 하나 서버를 암호 해독 하 고 팜의 다른 서버에서 유효성을 검사할 수 있습니다.
- **응용 프로그램 티켓 공유 교차** -단일 웹 서버는 여러 ASP.NET 응용 프로그램을 호스팅할 수 있습니다. 이러한 다른 응용 프로그램의 단일 폼 인증 티켓을 공유 해야 할 경우 반드시 해당 암호화 및 유효성 검사 키 맞춰야 합니다.

웹 팜 설정 하거나 동일한 서버에 응용 프로그램에서 인증 티켓을 공유를 사용할 때는 구성 해야 합니다는 &lt;machineKey&gt; 영향을 받는 응용 프로그램의 요소를 자신의 decryptionKey 및 validationKey 값이 일치 합니다.

위의 시나리오 중 어느 샘플 응용 프로그램에 적용 되지만, 우리 여전히 명시적 decryptionKey 및 validationKey 값을 지정 하 고 정의할 수 알고리즘을 사용할 수 있습니다. 추가 &lt;machineKey&gt; Web.config 파일에 설정 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

자세한 내용은 체크 아웃 [방법: ASP.NET 2.0에서 MachineKey 구성](https://msdn.microsoft.com/library/ms998288.aspx)합니다.

> [!NOTE]
> DecryptionKey 및 validationKey 값에서 발췌 한 것 [Steve Gibson](http://www.grc.com/stevegibson.htm)의 [완벽 한 암호 웹 페이지](https://www.grc.com/passwords.htm), 각 페이지 방문에 임의의 16 진수 문자 64을 생성 합니다. 프로덕션 응용 프로그램에 자체 방식을 만들지 이러한 키의 가능성을 줄이기 위해 완벽 한 암호 페이지에서 임의로 생성 된 값과 위의 키를 대체 하는 것이 좋습니다.


## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>티켓의 추가 사용자 데이터를 저장 하는 4 단계:

많은 웹 응용 프로그램에 대 한 정보를 표시 하거나 현재 로그온된 한 사용자를 기준으로 페이지의 표시 합니다. 예를 들어 웹 페이지는 사용자의 이름 및 모든 페이지의 맨 위에 있는 마지막 로그온 날짜를 표시할 수 있습니다. 폼 인증 티켓 현재 로그온된 한 사용자의 사용자 이름을 저장 하지만 페이지 인증 티켓에 저장 되지 않은 정보를 조회 하는 사용자-데이터베이스-저장소로 이동 해야 다른 정보가 필요할 때.

약간의 코드 사용에서는 폼 인증 티켓의 추가 사용자 정보를 저장할 수 있습니다. 통해 이러한 데이터를 표시할 수는 [FormsAuthenticationTicket 클래스](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)의 [UserData 속성](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)합니다. 이 적은 양의 일반적으로 필요한 사용자에 대 한 정보를 저장 하는 유용한 장소가 있습니다. 속성의 인증 티켓 쿠키 하 고, 다른 티켓 필드와 같은 일부 포함 되어, 정책이 암호화 되어 유효성을 검사할 사용자 데이터에 지정 된 값 폼 인증 시스템 구성을 기반으로 합니다. 기본적으로 UserData은 빈 문자열입니다.

인증 티켓에 사용자 데이터를 저장 하기 위해 사용자 관련 정보를 가져와 고 티켓에 저장 하는 로그인 페이지에서 약간의 코드를 작성 해야 합니다. 사용자 데이터는 String 형식의 속성 이기 때문에 저장 된 데이터를 문자열로 제대로 직렬화 되어야 합니다. 예를 들어 사용자 저장소, 직원의 이름과 각 사용자의 생년월일을 포함 하 고 인증 티켓에 이러한 두 속성 값을 저장 한다고 가정 합니다. 고용주 이름을 파이프 (|)와 출생의 문자열의 사용자의 날짜를 연결 하 여 이러한 값을 문자열로 serialize 수 없습니다. 사용자의 1974 년 8 월 15에 태어난 Northwind Traders에 사용 중인 경우에서는 할당 UserData 속성 문자열: 1974-08-15 | Northwind Traders 합니다.

티켓에 저장 된 데이터에 액세스 해야 할 때마다 현재 요청 FormsAuthenticationTicket 위치와 UserData 속성을 역직렬화 그렇게 할 수 있습니다. 생년월일 및 고용주 이름 예제에서는 날짜의 경우 UserData 문자열 구분 기호 (|)에 따라 두 부분 문자열을 분할할 것 했습니다.


[![인증 티켓에 추가 사용자 정보를 저장할 수 있습니다.](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**그림 04**: 추가 사용자 정보에에서 저장할 수 인증 티켓 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png))


### <a name="writing-information-to-userdata"></a>사용자 데이터에 정보를 기록

그러나, 폼 인증 티켓에 사용자 관련 정보를 추가 된다고 예상 만큼 간단 수 없습니다. FormsAuthenticationTicket 클래스의 UserData 속성은 읽기 전용 이며 FormsAuthenticationTicket 클래스 생성자를 통해 지정할 수 있습니다. 또한 티켓의 다른 값을 제공 해야 UserData 속성을 생성자에 지정 하는 경우: 사용자 이름, 발급일, 만료, 및 등입니다. 이전 자습서에서 로그인 페이지를 만들 때이 모든을 수행해 줍니다에 의해 처리 되었는지 FormsAuthentication 클래스입니다. 사용자 데이터에는 FormsAuthenticationTicket를 추가할 때는 대부분의 FormsAuthentication 클래스에 의해 제공 기능을 복제 하는 코드를 작성 해야 합니다.

인증 티켓에 사용자에 대 한 추가 정보를 기록 Login.aspx 페이지를 업데이트 하 여 UserData로 작업 하는 데 필요한 코드를 살펴보겠습니다. 사용자가 스토어에 대 한 사용자가는 회사 및 해당 제목에 대 한 정보를 포함 하 고 인증 티켓에서이 정보를 캡처하려면 한다고 이라고 가정 합니다. 코드는 다음과 같이 표시 되도록 Login.aspx 페이지 LoginButton Click 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

한 번에 한 줄씩 코드가 단계별로 실행 해 보겠습니다. 메서드 4 개의 문자열 배열을 정의 하 여 시작: 사용자, 암호, companyName 및 titleAtCompany 합니다. 이러한 배열은 저장할 사용자 이름, 암호, 회사 이름 및 사용자 계정에 대 한 제목 시스템에서의 세 가지는: Scott, Jisun, 및 Sam 합니다. 실제 응용 프로그램에서 하지 하드 코드 된 페이지의 소스 코드에서 사용자 저장소에서 이러한 값은 쿼리할 수는.

이전 자습서에서 제공 된 자격 증명이 유효 하는 경우 단순히 호출을 다음 단계를 수행한 FormsAuthentication.RedirectFromLoginPage (UserName.Text, RememberMe.Checked):

1. 폼 인증 티켓 생성
2. 적절 한 저장소를에 티켓을 썼습니다. 쿠키 기반 인증 티켓에 대 한 브라우저의 쿠키 컬렉션을 사용 합니다. 티켓 데이터 URL로 serialize 되 쿠키 인증 티켓에 대 한
3. 사용자를 적절 한 페이지로 리디렉션됩니다.

이러한 단계는 위의 코드에 복제 됩니다. 첫째, 결국 UserData 속성에 저장할 문자열 회사 이름 및 두 개의 값을 파이프 문자 (|)과 구분 하는 제목, 결합 하 여 형성 됩니다.

Dim userDataString As String = String.Concat(companyName(i), "|", titleAtCompany(i))

다음으로, 인증 티켓을 만드는, FormsAuthentication.GetAuthCookie 메서드가 호출 되는 암호화 및 구성 설정에 따라 유효성 검사를 수행 하 고 HttpCookie 개체에 배치 합니다.

Dim authCookie As HttpCookie = FormsAuthentication.GetAuthCookie(UserName.Text, RememberMe.Checked)

쿠키 내에 포함 된 FormAuthenticationTicket를 사용 하려면 FormAuthentication 클래스를 호출 해야 [메서드 해독](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)쿠키 값에 전달 합니다.

Dim ticket As FormsAuthenticationTicket = FormsAuthentication.Decrypt(authCookie.Value)

그런 다음 만듭니다는 *새* FormsAuthenticationTicket 인스턴스 값을 기반으로 기존 FormsAuthenticationTicket의 합니다. 그러나이 새 티켓 사용자 관련 정보 (userDataString)에 포함 됩니다.

Dim newTicket As FormsAuthenticationTicket = New FormsAuthenticationTicket(ticket.Version, ticket.Name, ticket.IssueDate, ticket.Expiration, ticket.IsPersistent, userDataString)

에서는 다음 암호화 (및 유효성 검사)를 호출 하 여 새 FormsAuthenticationTicket 인스턴스는 [메서드 암호화](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx), 하며 authCookie에이 암호화 된 (및 유효성이 검사 된) 데이터를 다시 추가 합니다.

authCookie.Value = FormsAuthentication.Encrypt(newTicket)

마지막으로 authCookie 미리 컬렉션에 추가 되 고 GetRedirectUrl 메서드 호출 되어 사용자에 게 보낼를 적절 한 페이지 확인.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

이 코드의 모든 UserData 속성은 읽기 전용 이며 FormsAuthentication 클래스가 GetAuthCookie, SetAuthCookie, 또는 RedirectFromLoginPage 메서드에서 사용자 데이터 정보를 지정 하는 메서드를 제공 하지 않는 때문에 필요 합니다.

> [!NOTE]
> 쿠키 기반 인증 티켓의 사용자 관련 정보를 저장 하는 코드 검사 했습니다. 폼 인증 티켓을 URL로 직렬화 하는 작업을 담당 클래스는.NET Framework에 대 한 내부입니다. 말해서, 쿠키 없는 폼 인증 티켓의 사용자 데이터를 저장할 수 없습니다.


### <a name="accessing-the-userdata-information"></a>사용자 데이터 정보에 액세스

이 시점에서 각 사용자의 회사 이름과 title 속성에 저장 됩니다 폼 인증 티켓 UserData 로그인 할 때입니다. 사용자 저장소에 이동 하지 않고도이 정보를 모든 페이지에서 인증 티켓에서 액세스할 수 있습니다. 을 설명 하기 위해 UserData 속성에서이 정보를 검색할 수 있는 방법을 환영 메시지 뿐 아니라 사용자의 이름, 포함 하지만 또한에 대해 작동 하는 회사 제목에 Default.aspx를 업데이트 해 보겠습니다.

현재 Default.aspx 라는 WelcomeBackMessage 레이블 컨트롤과 AuthenticatedMessagePanel 패널을 포함 합니다. 이 패널은 인증 된 사용자에 게 표시 됩니다. Default.aspx의 페이지에서 코드를 업데이트\_을 다음과 같이 이벤트 처리기를 로드 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

Request.IsAuthenticated가 True 인 경우 WelcomeBackMessage의 Text 속성은 먼저 시작 뒤로 설정 *username*합니다. 그런 다음 기본 FormsAuthenticationTicket 액세스할 수 있도록 User.Identity 속성 FormsIdentity 개체 캐스팅 됩니다. FormsAuthenticationTicket 있으면, 회사 이름 및 제목으로 UserData 속성을 역직렬화 우리 합니다. 이 항목은 파이프 문자에서 문자열을 분할 하 여 수행 됩니다. 그러면 회사 이름 및 제목이 WelcomeBackMessage 레이블에 표시 됩니다.

그림 5에는 실행에서이 디스플레이의 스크린샷을 보여 줍니다. Scott로 로그인 Scott의 회사 및 제목을 포함 하는 환영 백 메시지를 표시 합니다.


[![현재 로그온 한 사용자의 회사 및 제목 표시](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**그림 05**: The 현재 로그온 한 사용자의 회사 및 제목 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png))


> [!NOTE]
> 인증 티켓 UserData 속성 사용자 저장소에 대 한 캐시 역할을 합니다. 모든 캐시와 같은 기본 데이터가 수정 될 때 업데이트 해야 합니다. 예를 들어 사용자가 자신의 프로필을 업데이트할 수 있는 웹 페이지 이면 UserData 속성에 캐시 필드 사용자가 수행한 변경 내용을 반영 하도록 새로 고쳐야 합니다.


## <a name="step-5-using-a-custom-principal"></a>5 단계: 사용자 지정 보안 주체를 사용 하 여

들어오는 각 요청은 FormsAuthenticationModule 사용자 인증을 시도 합니다. 만료 되지 않은 인증 티켓이 있는 경우는 FormsAuthenticationModule HttpContext.User 속성 새 GenericPrincipal 개체에 할당 합니다. 이 GenericPrincipal 개체에 FormsIdentity 폼 인증 티켓에 대 한 참조를 포함 하는 유형의 Id입니다. IPrincipal 구현 하는 클래스에 필요한 최소 운영 체제 미 설치 기능을 포함 하는 GenericPrincipal 클래스-IsInRole 방법과 Identity 속성에 있습니다.

주요 개체는 두 가지가: 사용자가 속한 역할을 지정 하 고 id 정보를 제공 합니다. 시키는 방법을 IPrincipal 인터페이스 IsInRole (*roleName*) 메서드와 Identity 속성을 각각. GenericPrincipal 클래스를 해당 생성자;를 통해 지정 해야 역할 이름의 문자열 배열에 대 한 허용 합니다. 해당 IsInRole (*roleName*) 검사 있는지 전달 된에서 *roleName* 문자열 배열 내에 있습니다. FormsAuthenticationModule 만듭니다는 GenericPrincipal, 빈 문자열 배열을 GenericPrincipal의 생성자에 전달 합니다. 따라서 IsInRole 호출할 때 항상 False를 반환 합니다.

GenericPrincipal 클래스에는 역할이 사용 되지 않습니다는 대부분의 양식 기반된 인증 시나리오에 대 한 요구 사항을 충족 합니다. 기본 역할 처리 충분 하지 않은 경우를 위해 있고 사용자 지정 IIdentity 개체를 사용자와 연결 해야 할 때 인증 워크플로 중 사용자 지정 IPrincipal 개체를 만들 HttpContext.User 속성에 할당 합니다.

> [!NOTE]
> 자습서, 나중에 알 수 있듯이 때 ASP 합니다. NET의 역할 프레임 워크가 활성화 형식의 사용자 지정 보안 주체 개체를 만듭니다 [RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx) 폼 인증에서 만든 GenericPrincipal 개체를 덮어씁니다. 역할 프레임 워크의 API와 상호 작용 하는 보안 주체의 IsInRole 메서드를 사용자 지정 하기 위해 수행 합니다.


우리는 신경 쓰지 직접 역할 아직, 이후 시점에 사용자 지정 보안 주체를 만들기 위한 있다고 하는 유일한 이유는 보안 주체에는 사용자 지정 IIdentity 개체에 연결할 것입니다. 4 단계에서에서 사용자의 회사 이름과 직책이 특히에서 인증 티켓 UserData 속성에 추가 사용자 정보를 저장 살펴보았습니다. 그러나 UserData 정보를만 인증 티켓을 통해 액세스할 수만 다음 serialize 된 문자열로 서, 티켓에 저장 된 사용자 정보를 보려면 원하는 언제 든 지 해야 한다는 사실을 UserData 속성을 구문 분석을 의미 합니다.

IIdentity를 구현 하 고 CompanyName 및 제목 속성을 포함 하는 클래스를 만들어 개발자 환경을 개선할 수 있습니다. 이런 방식으로 개발자 현재 로그온된 한 사용자의 회사 이름에 액세스할 수 및 없이 CompanyName 및 Title 속성을 통해 직접 제목 필요한 UserData 속성을 구문 분석 하는 방법에 알아야 합니다.

### <a name="creating-the-custom-identity-and-principal-classes"></a>사용자 지정 Id 및 주 클래스 만들기

이 자습서에 대 한 만들기는 사용자 지정 보안 주체 개체 및 identity 개체 응용 프로그램에서\_코드 폴더입니다. 응용 프로그램을 추가 하 여 시작\_폴더를 프로젝트 코드-솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, ASP.NET 폴더 추가 옵션을 선택 하 고 응용 프로그램을 선택\_코드입니다. 응용 프로그램\_코드 폴더는 웹 사이트에 특정 클래스 파일을 보유 하는 특별 한 ASP.NET 폴더입니다.

> [!NOTE]
> 응용 프로그램\_코드 폴더를 통해 웹 사이트 프로젝트 모델 프로젝트를 관리 하는 경우에 사용 해야 합니다. 사용 하는 경우는 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/asp.net/Aa336618.aspx), 표준 폴더를 만들고 있는 클래스에 추가 합니다. 예를 들어, 클래스, 라는 새 폴더를 추가 하 고 코드에 놓일 수 없습니다.


다음으로 응용 프로그램에 새 클래스 파일을 두 개를 추가\_코드 폴더, 하나의 명명 된 CustomIdentity.vb 개와 라는 CustomPrincipal.vb 합니다.


[![프로젝트에 CustomIdentity와 CustomPrincipal 클래스 추가](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**그림 06**: CustomIdentity와 CustomPrincipal 클래스를 프로젝트에 추가 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png))


CustomIdentity 클래스는 AuthenticationType, IsAuthenticated, 및 이름 속성을 정의 하는 IIdentity 인터페이스를 구현 하는 일을 담당 합니다. 이 이러한 필수 속성 외에도 연습에서는 기본 폼 인증 티켓으로 사용자의 회사 이름과 제목에 대 한 속성을 노출 합니다. CustomIdentity 클래스에 다음 코드를 입력 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

클래스 FormsAuthenticationTicket 멤버 변수를 포함 하는 참고 (\_티켓) 생성자를 통해이 티켓 정보를 제공 해야 하 고 있습니다. 이 티켓 데이터 반환 하므로 id의 Name;에 사용 됩니다. CompanyName 및 Title 속성에 대 한 값을 반환 하 고 UserData 속성 구문 분석 됩니다.

다음으로 CustomPrincipal 클래스를 만듭니다. CustomPrincipal 클래스의 생성자가 CustomIdentity 개체만; 허용 것은 문제가 되지 않습니다 역할 시점, 이후 IsInRole 메서드는 항상 False를 반환합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>들어오는 요청의 보안 컨텍스트 CustomPrincipal 개체 할당

했습니다 CompanyName 및 제목 속성을 포함 하도록 기본 IIdentity 사양을 확장 하는 클래스 뿐만 아니라 사용자 지정 id를 사용 하는 사용자 지정 주 클래스입니다. ASP.NET 파이프라인에 단계를 준비 하 고 수신 요청의 보안 컨텍스트를이 사용자 지정 보안 주체 개체를 할당 합니다.

ASP.NET 파이프라인 들어오는 요청을 사용 하 고 몇 가지 단계를 통해 처리 합니다. 각 단계에서 특정 이벤트 발생 ASP.NET 파이프라인에 간단 하 고 해당 수명 주기 전체에서 특정 시점에서 요청을 수정 하는 개발자를 위한 수 있도록 합니다. FormsAuthenticationModule 시키려면 ASP.NET에 대 한 예를 들어 대기는 [AuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), 어느 지점에서 인증 티켓에 대 한 들어오는 요청 검사 합니다. 인증 티켓 있더라도 GenericPrincipal 개체가 생성 되 고 HttpContext.User 속성에 할당 합니다.

ASP.NET 파이프라인 AuthenticateRequest 이벤트를 발생 시킵니다는 [PostAuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)역할의 인스턴스와 FormsAuthenticationModule에서 만든 GenericPrincipal 개체를 바꿀 수 있습니다는 우리의 CustomPrincipal 개체입니다. 그림 7이이 워크플로 보여 줍니다.


[![GenericPrincipal PostAuthenticationRequest 이벤트에서 CustomPrincipal으로 대체 됩니다.](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**그림 07**: The GenericPrincipal PostAuthenticationRequest 이벤트에서 CustomPrincipal으로 대체 됩니다 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png))


를 ASP.NET 파이프라인 이벤트에 대 한 응답에서 코드를 실행 하기 위해 म Global.asax에 적절 한 이벤트 처리기를 만들고 하거나 고유한 HTTP 모듈을 만들어야 합니다. 이 자습서에 대 한 Global.asax에 이벤트 처리기를 만들어 보겠습니다. 먼저 Global.asax 웹 사이트에 추가 합니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 Global.asax 라는 전역 응용 프로그램 클래스 형식의 항목을 추가 합니다.


[![Global.asax 파일을 웹 사이트 추가](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**그림 08**: Global.asax 파일을 웹 사이트 추가 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png))


시작, 끝을 포함 하 여 ASP.NET 파이프라인 이벤트 수에 대 한 이벤트 처리기를 포함 하는 기본 Global.asax 서식 파일 및 [오류 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx), 등입니다. 자유롭게에이 응용 프로그램에 필요 하지 않은 것 처럼 이러한 이벤트 처리기를 제거 합니다. 이 연습 이벤트 PostAuthenticateRequest입니다. 해당 태그와 다음과 유사 하므로 Global.asax 파일을 업데이트 합니다.

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

응용 프로그램\_OnPostAuthenticateRequest 메서드가 실행 될 때마다 ASP.NET 런타임이 들어오는 각 페이지 요청에서 한 번 수행 PostAuthenticateRequest 이벤트를 발생 시킵니다. 이벤트 처리기를 확인 하는 사용자가 인증 한 폼 인증을 통해 인증 되 고 시작 합니다. 이 경우에 새 CustomIdentity 개체가 생성 되 고 현재 요청 인증 티켓의 생성자에 전달 합니다. 그런 다음, CustomPrincipal 개체를 만들고 CustomIdentity 방금 만든 개체의 생성자에 전달 합니다. 마지막으로, 현재 요청의 보안 컨텍스트는 새로 만든된 CustomPrincipal 개체에 할당 됩니다.

-요청의 보안 컨텍스트를 CustomPrincipal 개체 연결-마지막 단계는 두 개의 속성에 보안 주체를 매기는 참고: HttpContext.User 및 Thread.CurrentPrincipal 합니다. 이러한 두 할당은 ASP.NET에서 처리 되는 보안 컨텍스트는 방식 때문에 필요 합니다. .NET Framework 보안 컨텍스트는 각 실행 스레드;에 연결 이 정보를 통해 IPrincipal 개체로 사용할 수는 [스레드 개체](https://msdn.microsoft.com/library/system.threading.thread.aspx)의 [CurrentPrincipal 속성](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)합니다. 혼란 스 러는 ASP.NET에는 자체 보안 컨텍스트 정보 (HttpContext.User)입니다.

특정 시나리오에서 Thread.CurrentPrincipal 속성을 보안 컨텍스트를 결정할 때 검사 다른 시나리오에서는 HttpContext.User 사용 됩니다. 예를 들어 사용자가 선언적으로 지정할 수 있는 보안 기능이.net에서 또는 역할 클래스를 인스턴스화할 수 특정 메서드를 호출 하거나 (참조 [업무 및 사용 하 여 데이터 계층에 권한 부여 규칙 추가 PrincipalPermissionAttributes](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)). 다음과 같은 선언적 방법을 내부적 Thread.CurrentPrincipal 속성을 통해 보안 컨텍스트를 결정 합니다.

다른 시나리오에서는 HttpContext.User 속성이 사용 됩니다. 예를 들어 이전 자습서에서 사용이 속성에서 현재 로그온 된 사용자의 사용자 이름을 표시 하려면. 명확 하 게 하는 것이 보안 컨텍스트 정보 Thread.CurrentPrincipal 및 HttpContext.User 속성에 맞춰 명령입니다.

ASP.NET 런타임 us에 대 한 이러한 속성 값을 자동으로 동기화 됩니다. 그러나이 동기화 AuthenticateRequest 이벤트 후에 발생 하지만 *전에* PostAuthenticateRequest 이벤트입니다. 따라서 PostAuthenticateRequest 이벤트에 사용자 지정 보안 주체를 추가 하는 경우 반드시 수동으로 Thread.CurrentPrincipal 또는 else Thread.CurrentPrincipal을 할당 해야 하 고 HttpContext.User 동기화 됩니다. 참조 [Context.User vs. Thread.CurrentPrincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) 에 대 한 자세한 내용은이 문제입니다.

### <a name="accessing-the-companyname-and-title-properties"></a>CompanyName 및 제목 속성에 액세스

요청이 도착 하 고 ASP.NET 엔진 응용 프로그램에 디스패치할 때마다\_Global.asax에 OnPostAuthenticateRequest 이벤트 처리기는 발생 합니다. 요청은 FormsAuthenticationModule 하 여 인증 되 면 이벤트 처리기는 폼 인증 티켓을 기반으로 하는 CustomIdentity 개체와 새 CustomPrincipal 개체를 만듭니다. 위치에이 논리를 사용 하 여 현재 로그온된 한 사용자의 회사 이름과 제목에 대 한 정보에 액세스 하는 매우 간단 합니다.

페이지로 돌아가\_Default.aspx, 여기서 4 단계에서에서 안내 드린 바 폼 인증 티켓을 검색 한 사용자의 회사 이름 및 제목 표시 하기 위해 UserData 속성을 구문 분석 하는 코드에서에서 이벤트 처리기를 로드 합니다. 사용 이제 CustomPrincipal 및 CustomIdentity 개체와 티켓의 UserData 속성에서 값을 구문 분석 하지 않아도가 됩니다. 대신, 단순히 CustomIdentity 개체에 대 한 참조를 가져오고 CompanyName 및 제목 속성을 사용 하 여:

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>요약

이 자습서에서 Web.config 통해 폼 인증 시스템 설정을 사용자 지정 하는 방법을 검사 했습니다. 인증 티켓이 만료를 처리 하는 방법을 고 검사 및 수정 된 티켓을 방지 하기 위해 암호화 및 유효성 검사 보호 기능을 사용 하는 방법 살펴보았습니다. 마지막으로 인증 티켓 UserData 속성을 사용 하 여 자체 티켓의 추가 사용자 정보와 사용자 지정 보안 주체 및 identity 개체를 사용 하 여 더 개발자에 게 친숙 한 방식으로이 정보를 노출 하는 방법을 저장 하 설명 합니다.

이 자습서는 asp.net에서 폼 인증 검사를 완료 했습니다. 다음 자습서 구성원 프레임 워크에이 작업을 시작합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [폼 인증 나누어서](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [ASP.NET 2.0에서에서 폼 인증 설명이 나와 있습니다.](https://msdn.microsoft.com/library/aa480476.aspx)
- [방법: ASP.NET 2.0에서에서 폼 인증을 보호](https://msdn.microsoft.com/library/ms998310.aspx)
- [전문 ASP.NET 2.0 보안, 구성원 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [로그인 컨트롤 보안](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;forms&gt; 요소에 대 한 &lt;인증&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [폼 인증 티켓 및 쿠키 이해](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 교육

- [폼 인증 속성을 변경 하는 방법](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [ASP.NET 응용 프로그램에서 쿠키 없는 인증을 설정 및 사용 하는 방법](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 폼 로그인 재배치](../../../videos/authentication/asp-forms-login-relocation.md)
- [폼 로그인 사용자 지정 키 구성](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [인증 방법에 사용자 지정 데이터 추가](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [사용자 지정 보안 주체 개체 사용](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

>[!div class="step-by-step"]
[이전](an-overview-of-forms-authentication-vb.md)
