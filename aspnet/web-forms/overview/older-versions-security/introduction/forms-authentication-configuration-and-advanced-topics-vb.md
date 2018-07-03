---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: 폼 인증 구성 및 고급 항목 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 다양 한 폼 인증 설정을 검사 하 고 폼 요소를 통해 수정 하는 방법을 참조 하세요. 자세한 수반 됩니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/14/2008
ms.topic: article
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: 493cb81271ea1c0439f7b499c5b48e659d3589b5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390863"
---
<a name="forms-authentication-configuration-and-advanced-topics-vb"></a>폼 인증 구성 및 고급 항목 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> 이 자습서에서는 다양 한 폼 인증 설정을 검사 하 고 폼 요소를 통해 수정 하는 방법을 참조 하세요. 이 작업을 자세히 살펴보고 사용자 지정 URL (예: SignIn.aspx Login.aspx 대신) 및 쿠키 없는 폼 인증 티켓을 사용 하 여 로그인 페이지를 사용 하 여 폼 인증 티켓 시간 제한 값을 사용자 지정 수반 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](an-overview-of-forms-authentication-vb.md) 에서 로그인 페이지를 표시 하려면 다른 만들지를 Web.config의 구성 설정을 지정 하는 ASP.NET 응용 프로그램에서 폼 인증을 구현 하는 데 필요한 단계에 살펴보았습니다 인증 및 익명 사용자에 대 한 내용입니다. Mode 특성을 설정 하 여 폼 인증을 사용 하려면 웹 사이트를 구성 하는 것을 기억 합니다 &lt;인증&gt; Forms 요소입니다. 합니다 &lt;인증&gt; 요소를 선택적으로 포함할 수는 &lt;forms&gt; 자식 요소에는 다양 한 폼 인증 설정을 지정할 수 있습니다.

이 자습서에서는 다양 한 폼 인증 설정 검사를 통해 수정 하는 방법은 합니다 &lt;forms&gt; 요소입니다. 이 작업을 자세히 살펴보고 사용자 지정 URL (예: SignIn.aspx Login.aspx 대신) 및 쿠키 없는 폼 인증 티켓을 사용 하 여 로그인 페이지를 사용 하 여 폼 인증 티켓 시간 제한 값을 사용자 지정 수반 합니다. 또한 폼 인증 티켓의 전반적을 좀 더 자세히 검토 하 고 ASP.NET 티켓의 데이터를 검사 및 변조 로부터 보호 하는 데 주의 참조 하세요. 마지막으로 폼 인증 티켓에 추가 되는 사용자 데이터를 저장 하는 방법 및 사용자 지정 보안 주체 개체를 통해이 데이터를 모델링 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>1 단계: 검사 합니다 &lt;forms&gt; 구성 설정

Asp.net에서 폼 인증 시스템은 다양 한 응용 프로그램 단위로 지정할 수 있는 구성 설정 제공 합니다. 와 같은 설정이 포함 됩니다: 폼 인증의 수명 동안 티켓; 어떤 종류의 보호 티켓;에 적용 됩니까 어떤 조건 쿠키 없는 인증 티켓이 사용 됩니다. 로그인 페이지 경로 및 기타 정보입니다. 기본 값을 수정 하려면를 [ &lt;forms&gt; 요소](https://msdn.microsoft.com/library/1d3t3c61.aspx) 의 자식으로는 [ &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx), 해당 속성을 지정 값을 XML 특성으로 사용자 지정 하려면 다음과 같이 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

표 1을 통해 사용자 지정할 수 있는 속성을 요약 합니다 &lt;forms&gt; 요소입니다. Web.config XML 파일 이므로 왼쪽된 열에 특성 이름이 대/소문자 구분 됩니다.


| <strong>특성</strong> |                                                                                                                                                                                                                                     <strong>설명</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         쿠키         |                                                                                                                이 특성은 어떤 조건에서 인증 티켓 및 URL에 포함 되는 쿠키에 저장 됩니다 지정 합니다. 허용 되는 값은: UseCookies; UseUri; 자동 검색 합니다. 및 UseDeviceProfile (기본값)입니다. 2 단계는이 설정을 자세히 검사합니다.                                                                                                                |
|         defaultUrl         |                                                                                                                                                         쿼리 문자열에 지정 된 RedirectUrl 값이 없을 경우 로그인 페이지에서 로그인 한 후에 사용자가 리디렉션되는 URL을 나타냅니다. 기본값은 default.aspx입니다.                                                                                                                                                         |
|           도메인           | 쿠키 기반 인증 티켓을 사용할 경우이 설정은 쿠키의 도메인 값을 지정 합니다. 기본값은 빈 문자열입니다 (예: www.yourdomain.com) 발급 된 도메인을 사용 하 여 브라우저는 합니다. 쿠키는이 예에서 <strong>되지</strong> admin.yourdomain.com 같은 하위 도메인을 위해 요청 하면 전송 합니다. 모든 하위 도메인에 전달할 쿠키를 하려는 경우 yourdomain.com로 설정 하는 도메인 특성을 사용자 지정 해야 합니다. |
|  enableCrossAppRedirects   |                                                                                                                                                                   인증 된 사용자는 동일한 서버의 다른 웹 응용 프로그램의 Url로 리디렉션할 때를 기억할지 여부를 나타내는 부울 값입니다. 기본값은 false입니다.                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      로그인 페이지의 URL입니다. 기본값은 login.aspx입니다.                                                                                                                                                                                                                      |
|            name            |                                                                                                                                                                                                   때 쿠키 기반 인증을 사용 하 여 티켓을 쿠키의 이름입니다. 기본값은입니다. ASPXAUTH 합니다.                                                                                                                                                                                                   |
|            path            |                                                                             쿠키 기반 인증 티켓을 사용할 경우이 설정은 쿠키 s path 특성을 지정 합니다. Path 특성에는 개발자를 특정 디렉터리 계층 구조를 쿠키의 범위를 제한할 수 있습니다. 기본값은 / 도메인에 대 한 모든 요청에서 인증 티켓 쿠키를 보낼 브라우저에 게 알립니다.                                                                              |
|         보호         |                                                                                                                                            폼 인증 티켓을 보호 하기 위해 어떤 기술이 사용 되는지 나타냅니다. 허용 되는 값은: 모두 (기본값). 암호화 해당 항목이 없습니다. 및 유효성 검사 합니다. 이러한 설정에 대해서는 3 단계에서에서 자세히 설명 합니다.                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                SSL 연결을 인증 쿠키를 전송 해야 하는지 여부를 나타내는 부울 값입니다. 기본값은 false입니다.                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 사용자가 단일 세션에서 사이트를 방문할 때마다 인증 쿠키가 시간 초과 다시 설정 하는지 여부를 나타내는 부울 값입니다. 기본값은 true입니다. 인증 티켓 시간 제한 정책 지정은에서 더 자세히 설명 되어 티켓 시간 제한 값 섹션 s입니다.                                                                                                 |
|          시간 제한           |                                                                                                                               인증 티켓 쿠키 만료 되는 분 단위로 시간을 지정 합니다. 기본값은 30입니다. 인증 티켓 시간 제한 정책 지정은에서 더 자세히 설명 되어 티켓 시간 제한 값 섹션 s입니다.                                                                                                                               |

**표 1**: A 요약이 합니다 &lt;forms&gt; 요소의 특성

ASP.NET 2.0 이상에서 기본.NET Framework의 FormsAuthenticationConfiguration 클래스에서 하드 코드 된 폼 인증 값은입니다. Web.config 파일에서 응용 프로그램 단위로 수정 적용 되어야 합니다. ASP.NET에서이 반해 1.x의 경우 여기서 forms 인증 기본값 합니다 machine.config 파일에 저장 된 (및 따라서 machine.config를 편집을 통해 수정 될 수 있습니다). ASP.NET의 항목에는 while 1.x 가치가 언급 다양 한 폼 인증 시스템 설정 ASP.NET 2.0의 다른 기본 값이 있다고 이상 보다 asp.net에서 1.x 합니다. ASP.NET 1.x 환경에서 응용 프로그램을 마이그레이션하려는 경우에 이러한 차이점에 유의 해야 합니다. 참조 하세요 [는 &lt;forms&gt; 요소 기술 설명서](https://msdn.microsoft.com/library/1d3t3c61.aspx) 차이점 목록은 합니다.

> [!NOTE]
> 시간 제한, 도메인, 경로 등의 여러 폼 인증 설정 결과 폼 인증 티켓 쿠키에 대 한 세부 정보를 지정 합니다. 쿠키, 그 작동 방법 및 다양 한 속성에 대 한 자세한 내용은 읽을 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)합니다.


### <a name="specifying-the-tickets-timeout-value"></a>티켓의 시간 제한 값 지정

폼 인증 티켓에는 id를 나타내는 토큰입니다. 쿠키 기반 인증 티켓을 사용 하 여이 토큰은 쿠키 형식에 저장 되 고 각 요청에서 웹 서버로 전송 합니다. 토큰 소유 본질적으로 선언, 저는 *username*, 이미 로그인 했는지 그리고 방문 페이지에서 사용자의 id를 저장할 수 있습니다 하는 데 사용 됩니다.

폼 인증 티켓을 사용자의 id를 포함 합니다. 뿐만 아니라도 무결성 및 보안 토큰을 확인 하는 데 유용한 정보가 포함 되어 있습니다. 결국을 돌파 지요 토큰 underhanded 어떤 방식으로든에서 수정 또는 불법 토큰을 만들 수 있게 되기를 원하지 합니다.

한 이러한 티켓에 포함 된 정보의 비트가 *만료*, 날짜 및 시간 티켓 더 이상 유효 합니다. Formsauthenticationmodule은 인증 티켓, 검사 될 때마다 티켓의 만료 아직 경과 하지 않은 확인 합니다. 가 있는 경우 티켓을 무시 하 고 익명으로 사용자를 식별 합니다. 이 보호는 재생 공격 으로부터 보호 하는 데 도움이 됩니다. 해커가 자신의 컴퓨터에 물리적 액세스를 응원 하는 쿠키를 통해 아마도 자신의 실습-사용자의 유효한 인증 티켓을 가져올 수-이 도난당 한 인증 티켓을 사용 하 여 서버에 요청을 보낼 수 있는 경우에 만료 없이 및 항목을 얻을 수 있습니다. 만료 되지 않습니다이 시나리오를 방지 하는 동안 이러한 공격이 성공할 수 있는 창을 제한지 않습니다.

> [!NOTE]
> 인증 티켓을 보호 하기 위해 폼 인증 시스템에서 사용 하는 세부 정보 추가 기술의 3 단계.


인증 티켓을 만들 때 시간 제한 설정을 참조 하 여 해당 만료를 결정 하는 폼 인증 됩니다. 표 1에 설정이 기본적으로 30 분, 시간 제한에서 설명한 것 처럼 폼 인증 티켓을 만들면 해당 만료 날짜 및 시간 30 분에 나중에 설정 한다는 의미입니다.

만료를 절대 나중에 폼 인증 티켓이 만료 되는 시간을 정의 합니다. 하지만 개발자가 일반적으로 사용자는 사이트를 다시 검토 때마다 다시 설정 하는 상대 (sliding) 만료를 구현 하려고 합니다. 이 동작은 slidingExpiration 설정에 따라 결정 됩니다. 경우 true로 설정 (기본값), formsauthenticationmodule은 사용자를 인증할 때마다 업데이트 티켓의 만료 합니다. 각 요청에 만료 false로 설정 업데이트 되지 않으면, 티켓을 정확 하 게 시간 초과 수가 티켓이 처음 분 후 만료로 인해 생성 됩니다.

> [!NOTE]
> 만료 된 인증 티켓에 저장 된 절대 날짜 및 시간 값을 2008 년 8 월 2 일 오전 11시 34분와 같은 경우 또한 날짜 및 시간을 웹 서버의 현지 시간을 기준으로 됩니다. 이 디자인 결정에는 몇 가지 흥미로운 의도 주위 일광 절약 시간 (DST) 미국의 시계를 이동할 때 계속 해 서 1 (웹 서버가 호스팅되는 일광 절약 시간은 관찰 된 로캘의 가정)는 있을 수 있습니다. DST 시작 하는 시간을 30 분 만료를 사용 하 여 ASP.NET 웹 사이트에 대 한 상황 하는 것이 좋습니다 (위치인 2:00 AM). 방문자를 로그온 합니다. 사이트에 2008 년 3 월 11 일 오전 1 시 55 한다고 가정 합니다. 이 오전 2 시 25 (30 분에 나중에 해당) 2008 년 3 월 11 일에 만료 되는 폼 인증 티켓을 생성 합니다. 그러나 일단 2:00 AM 시점이, 시계 이동 3:00 AM DST 때문입니다. 사용자 (오전 3 시 01)에 로그인 한 후 6 분 후 새 페이지를 로드 하는 경우 FormsAuthenticationModule 정보 티켓 만료 하는 사용자를 로그인 페이지로 리디렉션합니다. 이 및 다른 인증 티켓 시간 제한 oddities, 뿐만 아니라 해결 방법에 대 한 더 상세히 논의 Stefan Schackow 복사본 선택할 *Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리* (ISBN: 978-0-7645-9698-8).


그림 1에서는 slidingExpiration가 false로 설정 하 고 제한 시간 30으로 설정 된 경우 워크플로 보여 줍니다. 로그인에서 생성 된 인증 티켓 만료 날짜를 포함 하 고 이후 요청에서이 값이 업데이트 되지 않습니다. Formsauthenticationmodule은 티켓이 만료 되었습니다 찾으면를 무시 하 고 익명으로 요청을 처리 합니다.


[![폼 인증 티켓이 만료 때 slidingExpiration의 그래픽 표현을 isfalse합니다](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**그림 01**:는 그래픽으로 폼 인증 티켓이 만료 때 slidingExpiration이 false ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png))


그림 2 slidingExpiration로 설정 된 경우 워크플로 보여 줍니다 true이 고 시간 제한을 30으로 설정 됩니다. (만료 되지 않은 ticket)를 포함 한 인증된 요청을 받으면 해당 만료 시간 (분) 이후에 시간 초과 수로 업데이트 됩니다.


[![폼 인증 티켓을 그래픽으로 표현한 slidingExpiration 참인 경우](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**그림 02**:는 폼 인증 티켓의 그래픽 표현을 slidingExpiration 그렇습니다 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png))


쿠키 기반 인증 티켓 (기본값)를 사용 하 여 쿠키에 지정 된 자신의 expiries 수도 있으므로이 토론 다소 혼동 됩니다. 쿠키의 만료 (또는 결핍) 쿠키를 제거 해야 하는 경우 브라우저에 지시 합니다. 쿠키 만료에 없는 경우 브라우저 종료 될 때 제거 됩니다. 그러나 만료가 있는 경우 쿠키 날짜까지에 사용자의 컴퓨터에 저장 하는 상태로 유지 됩니다 및 만료에 지정 된 시간이 경과 합니다. 브라우저에서 쿠키를 제거 하는 경우 더 이상 웹 서버에 전송 됩니다. 따라서 쿠키의 소멸은 사이트에서 로그 아웃이 사용자와 비슷합니다.

> [!NOTE]
> 물론, 사용자가 컴퓨터에 저장 된 모든 쿠키를 사전에 제거할 수 있습니다. Internet Explorer 7의 도구, 옵션로 이동 하는 검색 기록 섹션에서 삭제 단추를 클릭 합니다. 여기에서 쿠키 삭제 단추를 클릭 합니다.


Forms 인증 시스템에 전달 된 값에 따라 만료 기반 또는 세션 기반 쿠키를 만듭니다는 *persistCookie* 매개 변수입니다. FormsAuthentication 클래스의 GetAuthCookie, SetAuthCookie, 및 RedirectFromLoginPage 메서드는 두 개의 입력된 매개 변수에서 수행 하는 재현 율: *사용자 이름* 하 고 *persistCookie*합니다. 이전 자습서에서 만든 로그인 페이지에 암호 저장 확인란, 영구 쿠키가 만들어졌는지 여부를 결정 하는 포함 되어 있습니다. 영구 쿠키는 만료부터 시작 합니다. 비 영구적 쿠키는 세션 기반입니다.

이미 설명 된 제한 시간 및 slidingExpiration 개념 두 세션 및 만료 기반 쿠키를 적용할 동일 합니다. 실행에서만 가지 사소한 차이점이: 만료 기반 쿠키를 사용 하 여 true로 설정 된 slidingTimeout, 쿠키의 만료만 업데이트 됩니다 때 경과 지정 시간의 절반 이상.

상대 (sliding) 만료를 사용 하 여 시간 제한 (60 분)을 1 시간 후 티켓을 할당 하는 웹 사이트의 인증 티켓 시간 제한 정책 업데이트 해 보겠습니다. 이 변경 내용을 적용 하려면 Web.config 파일 업데이트 추가 &lt;forms&gt; 요소를 &lt;인증&gt; 요소를 다음 태그로:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Login.aspx 이외의 로그인 페이지 URL을 사용 하 여

Formsauthenticationmodule은 자동으로 리디렉션되므로 권한이 없는 사용자가 로그인 페이지를 로그인 페이지의 URL을 알고 있어야 합니다. LoginUrl 특성에서이 URL을 지정 합니다 &lt;forms&gt; 요소 및 기본값은 login.aspx입니다. 기존 웹 사이트를 통해 이식 하는 경우 이미 책갈피가 설정 및 검색 엔진에서 인덱스는 다른 URL 사용 하 여 로그인 페이지를 이미 있을 수도 있습니다. 기존 로그인 페이지에 login.aspx로 이름 바꾸기 및 주요 링크 및 사용자의 책갈피를 대신 로그인 페이지를 가리키도록 loginUrl 특성 대신 수정할 수 있습니다.

예를 들어 로그인 페이지 SignIn.aspx 이름이 사용자 디렉터리에 있는 가리킬 수 있습니다 ~/Users/SignIn.aspx에 loginUrl 구성 설정을 다음과 같이 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

없기 때문에 이미 현재 응용 프로그램에 Login.aspx 라는 로그인 페이지에서 사용자 지정 값을 지정 하지 않아도 합니다 &lt;forms&gt; 요소입니다.

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>쿠키 없는 폼 인증 티켓을 사용 하 여 2 단계:

기본적으로 폼 인증 시스템의 인증 티켓 쿠키 컬렉션에 저장 하거나 사이트를 방문 하는 사용자 에이전트 기반 URL에 포함할지 여부를 결정 합니다. 모든 주요 브라우저는 Internet Explorer, Firefox, Opera 및 Safari 지원 쿠키를 비슷하지만 모든 모바일 장치에서 수행.

Forms 인증 시스템에서 사용 된 쿠키 정책에서 쿠키 없는 설정에 따라 합니다 &lt;forms&gt; 네 값 중 하나로 지정할 수 있습니다. 요소:

- UseCookies-쿠키 기반 인증 티켓은 항상 사용할 수를 지정 합니다.
- UseUri-쿠키 기반 인증 티켓을 사용 하지 않을 것을 나타냅니다.
- 자동 검색-장치 프로필 쿠키 기반 인증 티켓 쿠키를 지원 하지 않는 경우 사용 되지 않습니다. 장치 프로필에서 쿠키를 지 원하는 경우 쿠키는 설정 되었는지 확인 하려면 검색 메커니즘이 사용 됩니다.
- UseDeviceProfile-기본값이 며 장치 프로필에서 쿠키를 지원 하는 경우에 쿠키 기반 인증 티켓을 사용 합니다. 검색 메커니즘이 사용 됩니다.

자동 검색 및 UseDeviceProfile 설정 사용을 *장치 프로필* 부분도 쿠키 기반 또는 쿠키 없는 인증 티켓을 사용할 것인지에 있습니다. ASP.NET의 다양 한 장치 및 쿠키를 지원 하는지 여부를, 버전, 지원 되는 JavaScript의 해당 기능에는 데이터베이스를 유지 합니다. 될 때마다 장치에서 웹 페이지를 따라 보냅니다 웹 서버에서 요청을 *사용자-에이전트* 장치 유형을 식별 하는 HTTP 헤더입니다. ASP.NET은 자동으로 해당 데이터베이스에 지정 된 해당 프로필을 사용 하 여 제공 된 사용자 에이전트 문자열을 일치 합니다.

> [!NOTE]
> 이 데이터베이스의 장치 기능을 준수 하는 여러 개의 XML 파일에에서 저장 됩니다는 [브라우저 정의 파일 스키마](https://msdn.microsoft.com/library/ms228122.aspx)합니다. 기본 장치 프로필 파일이 %WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers에서 있습니다. 응용 프로그램의 앱에 사용자 지정 파일을 추가할 수도 있습니다\_브라우저 폴더입니다. 자세한 내용은 [방법: ASP.NET 웹 페이지에서 브라우저 종류를 검색](https://msdn.microsoft.com/library/3yekbd5b.aspx)합니다.


기본 설정은 UseDeviceProfile 이기 때문에 장치 프로필이 쿠키를 지원 하지 않으면 보고 사이트를 방문 하는 경우 쿠키 없는 폼 인증 티켓 사용 됩니다.

### <a name="encoding-the-authentication-ticket-in-the-url"></a>URL에서 인증 티켓을 인코딩

쿠키는 브라우저에서 정보를 포함 하 여 기본 폼 인증 설정 방문 장치를 지 원하는 경우 쿠키를 사용 하는 이유는 특정 웹 사이트에 각 요청에 대 한 자연 스러운 보통입니다. 쿠키를 지원 하지 않는 경우 서버에 클라이언트에서 인증 티켓을 전달 하는 대체 방법을 채택 해야 합니다. 쿠키 없는 환경에서 사용 되는 일반적인 문제 해결 URL에 쿠키 데이터를 인코딩할 경우

참조 URL 내에서 이러한 정보를 포함할 수 있습니다 하는 방법에 대 한 가장 좋은 방법은 사이트 쿠키 없는 인증 티켓을 사용 하도록 하는 것입니다. UseUri 쿠키 없는 구성 설정을 설정 하 여이 수행할 수 있습니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

한 번이 변경 내용이 브라우저를 통해 사이트를 참조 하십시오. 익명 사용자로 방문 하면 Url 이전과 마찬가지로 정확 하 게 보입니다. 예를 들어, Default.aspx 페이지를 방문 하면 브라우저의 주소 표시줄에 다음 URL을 보여 줍니다.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

그러나 로그인 시 폼 인증 티켓이 URL에 포함 됩니다. 예를 들어 로그인 페이지를 방문 하 고에 Sam으로 로그인 한 후 Default.aspx 페이지로 반환 저는 필자 있지만 URL이 시간은:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

폼 인증 티켓은 URL 내의 포함 되었으면 합니다. 문자열 (F (jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv rfezq0gKadKX0YPZCkA2)는 일반적으로 쿠키에 저장 되는 동일한 데이터 및 16 진수로 인코딩된 인증 티켓 정보를 나타냅니다.

작동 하도록 쿠키 없는 인증 티켓에 대 한 순서 대로 시스템 인증 티켓 데이터를 포함 하려면 페이지의 모든 Url 인코딩해야 합니다., 그렇지 않으면 인증 티켓을 됩니다 손실 사용자가 링크를 클릭 합니다. 다행 스럽게도 포함이 논리는 자동으로 수행 됩니다. 이 기능을 보여 주기 위해 Default.aspx 페이지를 열고 테스트 링크를 SomePage.aspx, 해당 텍스트 및 NavigateUrl 속성을 각각 설정 하이퍼링크 컨트롤을 추가 합니다. 실제로 없다는 페이지 SomePage.aspx 라는 프로젝트에는 중요 하지 않습니다.

Default.aspx에 변경 내용을 저장 하 고 방문 하 여 브라우저를 통해 키를 누릅니다. 폼 인증 티켓이 URL에 포함 되어 있도록 사이트에 로그온 합니다. 그런 다음 Default.aspx를에서 링크 테스트 링크를 클릭 합니다. 어떻게 된 것입니까? SomePage.aspx 라는 페이지가 없는 경우 404 오류가 발생 한 후 이지만 하지 중요 한 것 같습니다. 대신, 브라우저의 주소 표시줄에 집중 합니다. URL에서 폼 인증 티켓을 포함 하는 참고!

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

링크의 URL SomePage.aspx 인증 티켓-를 포함 하는 URL에 자동으로 변환 된에서는 코드가 전혀 작성할 필요가 없었습니다! Http://로 시작 하지 않는 모든 하이퍼링크 URL에 자동으로 포함 될 폼 인증 티켓 또는 /. 하이퍼링크 Response.Redirect 호출, 하이퍼링크 컨트롤을 또는 HTML 앵커 요소에 나타나는 경우 문제가 되지 않습니다 (즉, &lt;a = "..."&gt;... &lt;/a&gt;). URL은 같은으로 http://www.someserver.com/SomePage.aspx 또는 /SomePage.aspx, 폼 인증 티켓에 포함 됩니다.

> [!NOTE]
> 쿠키 없는 폼 인증 티켓 쿠키 기반 인증 티켓으로 동일한 시간 제한 정책을 준수합니다. 그러나 쿠키 없는 인증 티켓은 인증 티켓을 URL에 직접 포함 되어 있으므로 재생 공격 하기 더 쉽습니다. Imagine 사용자는 웹 사이트를 방문 하 고, 로그인 후 동료에 게 전자 메일에 URL을 붙여 넣습니다. 동료는 만료에 도달 하기 전에 해당 링크를 클릭할 하는 경우 이러한로 기록 됩니다 전자 메일을 보낸 사용자에 게!


## <a name="step-3-securing-the-authentication-ticket"></a>3 단계: 보안 인증 티켓

폼 인증 티켓을 네트워크를 통해 전송 되 쿠키에 하나 또는 URL 내에서 직접 포함 합니다. Id 정보 외에도 인증 티켓이 포함 될 수 있습니다도 사용자 데이터 (4 단계에서에서 확인할 수)입니다. 따라서 것이 중요는 티켓의 데이터를 암호화할에서 침입자 (중요)는 forms 인증 시스템 티켓을 사용 하 여 손상 되지 않았음을 보장할 수 있습니다.

티켓의 데이터의 프라이버시 되도록 forms 인증 시스템에서 티켓 데이터를 암호화할 수 있습니다. 티켓 데이터를 암호화 하는 오류는 일반 텍스트로 네트워크를 통해 잠재적으로 중요 한 정보를 보냅니다.

티켓의 신뢰성을 보장 하기 위해 폼 인증 시스템 해야 *유효성 검사* 티켓입니다. 유효성 검사는 데이터의 특정 부분이 수정 되지 않았는지를 통해 수행 됩니다 유지 작업을  *[메시지 인증 코드 (MAC)](http://en.wikipedia.org/wiki/Message_authentication_code)* 합니다. 간단히 말해 MAC이 작은 부분 (이 여기서는 티켓)의 유효성을 검사 해야 하는 데이터를 식별 하는 정보입니다. MAC에서 표현 되는 데이터가 수정 되 면 다음 MAC 컴퓨터와 데이터는 일치 하지 않습니다. 또한는 모두 데이터를 수정 하 고 해당 하는 수정 된 데이터를 사용 하 여 자신의 MAC을 생성 해야 해커가 계산이 어렵습니다.

만드는 (또는 수정) 하는 경우 티켓을 forms 인증 시스템 MAC을 만들고 티켓의 데이터에 연결 합니다. 후속 요청이 도착 하면 폼 인증 시스템에서 티켓 데이터의 신뢰성이 유효한 지 유효성을 검사 하려면 MAC 및 티켓 데이터를 비교 합니다. 그림 3이이 워크플로 그래픽으로 보여 줍니다.


[![MAC을 통해 티켓의 신뢰성이 유효한 지 확인](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**그림 03**: MAC을 통해 The 티켓의 신뢰성 보장 됩니다 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png))


보호 설정에 따라 인증 티켓에는 보안 조치 적용 되는 &lt;forms&gt; 요소입니다. 보호 설정은 다음 세 값 중 하나에 할당할 수 있습니다.

- All-티켓은 암호화 및 디지털 서명 (기본값).
- 암호화-암호화가 적용 되어-없습니다 MAC이 생성 됩니다.
- None-티켓은 암호화도 아니고 디지털 서명 합니다.
- 유효성 검사-MAC에 생성 되지만 티켓 데이터를 일반 텍스트로 네트워크를 통해 전송 됩니다.

모든 설정을 사용 하는 것이 좋습니다.

### <a name="setting-the-validation-and-decryption-keys"></a>유효성 검사 및 암호 해독 키를 설정합니다.

암호화 및 해시를 암호화 하 여 인증 티켓의 유효성을 검사 forms 인증 시스템에서 사용 하는 알고리즘은을 통해 사용자 지정할 수는 [ &lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx) Web.config에서 있습니다. 표 2 윤곽선 합니다 &lt;machineKey&gt; 요소의 특성 및 가능한 값입니다.

| **특성** | **설명** |
| --- | --- |
| 해독 | 암호화에 사용 된 알고리즘을 나타냅니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다: 자동-기본값이 며 decryptionKey 특성의 길이 기반으로 하는 알고리즘을 결정 합니다. -AES-사용 된 [암호화 표준 AES (고급)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 알고리즘입니다. DES-사용 된 [표준 DES (데이터 암호화)](http://en.wikipedia.org/wiki/Data_Encryption_Standard) 이 알고리즘 계산이 약한 것으로 간주 됩니다 및 사용할 수 없습니다. -3DES-를 사용 하는 [Triple DES](http://en.wikipedia.org/wiki/Triple_DES) 세 번 DES 알고리즘을 적용 하 여 작동 하는 알고리즘입니다. |
| decryptionKey | 비밀 키 암호화 알고리즘을 사용 합니다. 이 값은 16 진수 문자열 (암호 해독 값에 따라) 적절 한 길이, AutoGenerate, 또는 추가 된 두 값 중 하나가 IsolateApps 합니다. 각 응용 프로그램에 대 한 고유한 값을 사용 하도록 ASP.NET을 지시 IsolateApps를 추가 합니다. 기본값은 AutoGenerate, IsolateApps. |
| 유효성 검사 | 유효성 검사에 사용 된 알고리즘을 나타냅니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다.-AES-표준 AES (고급 암호화) 알고리즘을 사용 합니다. -MD5-사용 된 [메시지 다이제스트 5 (MD5)](http://en.wikipedia.org/wiki/MD5) 알고리즘입니다. -SHA1-사용 된 [SHA1](http://en.wikipedia.org/wiki/Sha1) 알고리즘 (기본값). -3DES-Triple DES 알고리즘을 사용 합니다. |
| validationKey | 유효성 검사 알고리즘에서 사용할 비밀 키입니다. 이 값은 16 진수 문자열 (유효성 검사의 값에 따라) 적절 한 길이, AutoGenerate, 또는 추가 된 두 값 중 하나가 IsolateApps 합니다. 각 응용 프로그램에 대 한 고유한 값을 사용 하도록 ASP.NET을 지시 IsolateApps를 추가 합니다. 기본값은 AutoGenerate, IsolateApps. |

**표 2**: 합니다 &lt;machineKey&gt; 요소 특성

이러한 암호화 및 유효성 검사 옵션 및 전문가의 철저 한 설명과 단점 다양 한 알고리즘을이 자습서의 범위를 벗어납니다. 에 대 한 심층적인 확인을 사용 하려면 어떤 암호화 및 유효성 검사 알고리즘에 대 한 지침을 포함 하 여 이러한 문제를 어떤 키 길이 사용 하려면 이러한 키를 생성, 참조 하는 최선의 방법 및 *Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리* .

기본적으로 각 응용 프로그램에 대 한 암호화 및 유효성 검사에 사용 되는 키를 자동으로 생성 됩니다 하 고 이러한 키는 로컬 보안 기관 (LSA)에 저장 됩니다. 즉, 기본 설정을 웹 서버에서 웹 서버 및 응용 프로그램에서 응용 프로그램 별로 고유 키를 보장합니다. 따라서이 기본 동작은 다음 두 가지 시나리오에 대 한 작동 하지 않습니다.

- **웹 팜** -를 [웹 팜](http://en.wikipedia.org/wiki/Web_farm) 시나리오에서는 단일 웹 응용 프로그램 확장성 및 중복성을 위해 여러 웹 서버에서 호스팅됩니다. 들어오는 각 요청은 사용자의 세션 기간 동안 서로 다른 서버 수 사용할 수의 다양 한 요청을 처리 하는 팜의 서버에 디스패치 됩니다. 결과적으로 폼 인증 티켓을 만들 수 있도록 각 서버에서 동일한 암호화 및 유효성 검사 키를 사용 해야 합니다, 그리고 암호화 및에서 유효성이 검사 된 서버만 해독 하 고 팜의 다른 서버에서 유효성을 검사할 수 있습니다.
- **응용 프로그램 티켓 공유 간** -단일 웹 서버가 여러 ASP.NET 응용 프로그램을 호스팅할 수 있습니다. 이러한 다른 응용 프로그램의 단일 폼 인증 티켓을 공유 하는 경우 반드시 된 해당 암호화 및 유효성 검사 키가 일치 합니다.

웹 팜에 설정 하거나 동일한 서버에 응용 프로그램에서 인증 티켓을 공유를 사용할 때 구성 해야 합니다는 &lt;machineKey&gt; 영향을 받는 응용 프로그램의 요소를 해당 decryptionKey 및 validationKey 값 일치 합니다.

샘플 응용 프로그램에 적용 되는 위의 시나리오 중 어느 하는 동안 수 여전히 명시적 decryptionKey 및 validationKey의 값을 지정 하 고 사용할 알고리즘을 정의 합니다. 추가 된 &lt;machineKey&gt; Web.config 파일에 설정 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

자세한 내용은 체크 아웃 [방법: ASP.NET 2.0에서 MachineKey 구성](https://msdn.microsoft.com/library/ms998288.aspx)합니다.

> [!NOTE]
> DecryptionKey 및 validationKey 값에서 가져왔습니다 [Steve Gibson](http://www.grc.com/stevegibson.htm)의 [완벽 하 게 암호 웹 페이지](https://www.grc.com/passwords.htm), 각 페이지 방문에서 64 임의의 16 진수 문자를 생성 하 합니다. 프로덕션 응용 프로그램으로 이러한 키의 가능성을 줄이려면를 잘 모르는 완벽 한 암호 페이지에서 임의로 생성 된 것으로 위의 키를 바꿉니다.


## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>티켓의 추가 사용자 데이터를 저장 하는 4 단계:

많은 웹 응용 프로그램에 대 한 정보를 표시 하거나 현재 로그온된 한 사용자를 기준으로 페이지를 표시 합니다. 예를 들어, 웹 페이지는 사용자의 이름과 모든 페이지의 맨 위에 있는 마지막 로그온 날짜를 표시할 수 있습니다. 폼 인증 티켓을 현재 로그온된 한 사용자의 사용자 이름, 저장 하지만 페이지 인증 티켓에 저장 되지 않은 정보를 조회 하는 사용자-데이터베이스-저장소로 이동 해야 다른 정보, 필요한 경우.

약간의 코드를 사용 하 여 추가 사용자 정보 폼 인증 티켓에 저장할 수 있습니다. 이러한 데이터를 통해 표현 될 수 있습니다 합니다 [FormsAuthenticationTicket 클래스](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)의 [UserData 속성](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)합니다. 적은 양의 일반적으로 필요한 사용자에 대 한 정보를 저장 하기에 유용한 장소입니다. 속성의 인증 티켓 쿠키를 다른 티켓 필드와 같은 일부 포함 되어는 암호화 및 유효성 검사 userdata와 지정 된 값 forms 인증 시스템의 구성을 기반으로 합니다. 기본적으로 UserData 빈 문자열인 경우

인증 티켓에 사용자 데이터를 저장 하기 위해 사용자 고유의 정보를 가져와 티켓에 저장 하는 로그인 페이지에는 약간의 코드를 작성 해야 합니다. UserData 형식 문자열의 속성 이므로 문자열에 저장 된 데이터를 올바르게 직렬화 되어야 합니다. 예를 들어, 사용자 스토어가 고용주에 게 이름과 각 사용자의 생년월일이 포함 하는 인증 티켓의 이러한 두 속성 값을 저장 하려고 했습니다 한다고 가정 합니다. 고용주 이름 뒤에 사용자의 생년월일 파이프 (|)를 사용 하 여 생년월일의 문자열에 연결 하 여 문자열로 이러한 값을 직렬화 할 수 없습니다 했습니다. Northwind Traders에 대해 작동 하는 1974 년 8 월 15에서에서 탄생 하 게는 사용자에 대 한 할당 해야 UserData 속성 문자열: 1974-08-15 | Northwind Traders 합니다.

티켓에 저장 된 데이터에 액세스 해야 할 때마다 우리가 해결할 수 있으므로 현재 요청의 FormsAuthenticationTicket 위치와 UserData 속성을 역직렬화 합니다. 생년월일 및 고용주 이름 예의 날짜의 경우 구분 기호 (|)에 따라 두 문자열을 부분 UserData 문자열을 분할 됩니다.


[![인증 티켓의 추가 사용자 정보를 저장할 수 있습니다.](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**그림 04**: 추가 사용자 정보에에서 저장할 수 있습니다 인증 티켓 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png))


### <a name="writing-information-to-userdata"></a>사용자 데이터에 정보를 기록

그러나 폼 인증 티켓에 사용자 고유의 정보 추가 간단 하지 않습니다 예상할 수 있듯이 합니다. UserData FormsAuthenticationTicket 클래스의 읽기 전용인 지 속성과 FormsAuthenticationTicket 클래스 생성자를 통해 지정할 수 있습니다. 또한 티켓의 다른 값을 제공 해야 UserData 속성을 생성자에 지정 하는 경우: 사용자 이름, 발행일, 만료 및 등입니다. 이전 자습서에서 로그인 페이지를 만들었을 때이 모든 처리 되었는지에 FormsAuthentication 클래스입니다. 사용자 데이터에는 FormsAuthenticationTicket를 추가할 때 대부분 FormsAuthentication 클래스에 의해 이미 제공 하는 기능을 복제 하는 코드를 작성 해야 합니다.

인증 티켓에 사용자에 대 한 추가 정보를 기록 하려면 Login.aspx 페이지로 업데이트 하 여 사용자 데이터를 사용 하 여 작업에 필요한 코드를 살펴보겠습니다. 사용자 저장소에 대 한 사용자가 근무 하는 회사 및 직함에 대 한 정보를 포함 하 고 인증 티켓에이 정보를 캡처하려면 하려고 한다는 것으로 가정 합니다. 코드를 다음과 같이 표시 되도록 Login.aspx 페이지의 LoginButton Click 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

한 번에 코드 한 줄이 단계별로 실행 해 보겠습니다. 메서드 문자열 배열이 네 개 정의 하 여 시작: 사용자, 암호, companyName 및 titleAtCompany 합니다. 이러한 배열은 사용자 이름, 암호, 회사 이름 및 사용자 계정에 대 한 제목에에서 보관 시스템의 세 가지는: Scott, Jisun, 및 Sam입니다. 실제 응용 프로그램에서 이러한 값 하지 하드 코드 된 페이지의 소스 코드에서 사용자 저장소에서 쿼리할 수 됩니다.

이전 자습서에서 제공 된 자격 증명이 유효 하는 경우 단순히 호출 했습니다 다음 단계를 수행 하는 FormsAuthentication.RedirectFromLoginPage (UserName.Text, RememberMe.Checked):

1. 폼 인증 티켓 생성
2. 적절 한 저장소에 티켓을 기록합니다. 쿠키 기반 인증 티켓에 대 한 브라우저의 쿠키 컬렉션이 사용 됩니다. 티켓 데이터를 URL로 serialize 되 쿠키 없는 인증 티켓에 대 한
3. 사용자를 적절 한 페이지로 리디렉션됩니다.

이러한 단계는 위의 코드에서 복제 됩니다. 먼저 저장 하겠습니다. 결국 UserData 속성에 문자열을 회사 이름 및 파이프 문자 (|)를 사용 하 여 두 값을 구분 제목을 결합 하 여 형성 됩니다.

Dim userDataString As String = String.Concat(companyName(i), "|", titleAtCompany(i))

다음으로, 인증 티켓을 만드는 메서드를 호출 하면 FormsAuthentication.GetAuthCookie 암호화 구성 설정에 따라 유효성을 검사 및 HttpCookie 개체에 배치 합니다.

Dim authCookie As HttpCookie = FormsAuthentication.GetAuthCookie(UserName.Text, RememberMe.Checked)

쿠키에 포함 된 FormAuthenticationTicket를 사용 하려면 FormAuthentication 클래스를 호출 해야 [메서드를 암호 해독](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)쿠키 값을 전달 합니다.

Dim ticket As FormsAuthenticationTicket = FormsAuthentication.Decrypt(authCookie.Value)

그런 다음 만듭니다는 *새* FormsAuthenticationTicket 인스턴스 값을 기반으로 기존 FormsAuthenticationTicket의 합니다. 그러나이 새 티켓 (userDataString) 사용자별 정보를 포함합니다.

NewTicket으로 FormsAuthenticationTicket dim 새 FormsAuthenticationTicket(ticket. = 버전, 티켓입니다. 이름, 티켓입니다. IssueDate, 티켓입니다. 티켓 만료 합니다. IsPersistent userDataString)

그런 다음 암호화 (하 고 유효성 검사)를 호출 하 여 새 FormsAuthenticationTicket 인스턴스를 [암호화 메서드에](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx), authCookie에이 암호화 된 (및 유효성이 검사 된) 데이터를 다시 배치 하 고 합니다.

authCookie.Value = FormsAuthentication.Encrypt(newTicket)

마지막으로, authCookie 미리 컬렉션에 추가 하 고 사용자를 보낼 적절 한 페이지를 확인 하 GetRedirectUrl 메서드 호출 됩니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

이 코드를 모두 UserData 속성은 읽기 전용 및 FormsAuthentication 클래스는 해당 GetAuthCookie, SetAuthCookie, 또는 RedirectFromLoginPage 메서드에서 UserData 정보를 지정 하는 메서드를 제공 하지 않습니다 때문에 필요 합니다.

> [!NOTE]
> 쿠키 기반 인증 티켓의 사용자 관련 정보를 저장 하는 코드 검사 했습니다. URL로 폼 인증 티켓을 직렬화 하는 일을 담당 클래스는.NET framework 내부. 결론부터 말하자면, 쿠키 없는 폼 인증 티켓의 사용자 데이터를 저장할 수 없습니다.


### <a name="accessing-the-userdata-information"></a>UserData 정보에 액세스

이 시점에서 각 사용자의 회사 이름 및 title 속성에 저장 됩니다 폼 인증 티켓을 UserData 로그인 할 때입니다. 이 정보는 사용자 저장소를 이동 하지 않고도 모든 페이지에서 인증 티켓에서 액세스할 수 있습니다. 를 UserData 속성에서이 정보를 검색할 수 있는 방법을 보여 주기 위해 포함 하도록 해당 환영 메시지 뿐 아니라 사용자의 이름은 같지만 회사에 대 한 작동 및 직함 Default.aspx를 업데이트 해 보겠습니다.

현재 Default.aspx를 AuthenticatedMessagePanel 패널 WelcomeBackMessage 이라는 레이블 컨트롤을 포함 합니다. 이 패널은 인증 된 사용자에 게 표시 됩니다. Default.aspx의 페이지에서 코드를 업데이트\_다음과 같이 표시 되도록 이벤트 처리기를 로드 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

Request.IsAuthenticated가 True 인 경우 다시 시작 하려면 먼저 WelcomeBackMessage의 Text 속성 설정 됩니다 *username*합니다. 그런 다음 기본 FormsAuthenticationTicket 액세스할 수 있도록 User.Identity 속성 FormsIdentity 개체를 캐스팅 됩니다. FormsAuthenticationTicket 한 후 회사 이름 및 제목이으로 UserData 속성을 역직렬화 했습니다. 파이프 문자에서 문자열을 분할 하면 됩니다. 그러면 회사 이름 및 제목이 WelcomeBackMessage 레이블에 표시 됩니다.

그림 5에는 실행 중인이 디스플레이의 스크린샷을 보여 줍니다. Scott로 로그인 Scott의 회사 및 제목을 포함 하는 환영 백 메시지를 표시 합니다.


[![현재 로그온 한 사용자의 회사 및 제목 표시 됩니다.](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**그림 05**:은 현재 로그온 한 사용자의 회사 및 제목 표시 됩니다 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png))


> [!NOTE]
> 사용자 저장소에 대 한 캐시 된 인증 티켓의 UserData 속성이 제공 됩니다. 모든 캐시와 같은 기본 데이터가 수정 될 때 업데이트 해야 합니다. 예를 들어 사용자가 자신의 프로필을 업데이트할 수는 웹 페이지의 경우 UserData 속성에서 캐시 필드는 사용자가 변경한 내용을 반영 하도록 새로 고쳐야 합니다.


## <a name="step-5-using-a-custom-principal"></a>5 단계: 사용자 지정 보안 주체를 사용 하 여

들어오는 각 요청에 formsauthenticationmodule은 사용자를 인증 하려고 시도 합니다. 만료 되지 않은 인증 티켓을 있으면 formsauthenticationmodule은 새 GenericPrincipal 개체에 HttpContext.User 속성을 할당 합니다. 이 GenericPrincipal 개체에 FormsIdentity 폼 인증 티켓에 대 한 참조를 포함 하는 형식의 Id입니다. GenericPrincipal 클래스 IPrincipal을 구현 하는 클래스에 필요한 최소 운영 기능 포함-Identity 속성 및 IsInRole 메서드를가 하는 것입니다.

주요 개체는 두 가지 책임이: id 정보를 제공 하는 사용자가 속한 역할을 나타냅니다. 이 IPrincipal 인터페이스의 IsInRole을 통해 수행 됩니다 (*roleName*) 메서드와 Identity 속성을 각각. GenericPrincipal 클래스 생성자를 통해 지정할 역할 이름의 문자열 배열에 대 한 허용 합니다. 해당 IsInRole (*roleName*) 메서드는 단순히 있는지 검사 전달 된에서 *roleName* 문자열 배열 내에 존재 합니다. FormsAuthenticationModule은 GenericPrincipal를 만들고, 빈 문자열 배열을 GenericPrincipal의 생성자에 전달 합니다. 따라서 IsInRole 호출할 때 False를 항상 반환 됩니다.

GenericPrincipal 클래스 역할이 사용 되지 않습니다 하는 대부분의 양식 기반된 인증 시나리오에 대 한 요구 사항을 충족 합니다. 이러한 경우는 기본 역할 처리 부족 하거나 사용자를 사용 하 여 사용자 지정 IIdentity 개체를 연결 해야 할 때 인증 워크플로 중에 사용자 지정 IPrincipal 개체 만들기를 HttpContext.User 속성에 할당 합니다.

> [!NOTE]
> 자습서, 나중에 확인할 수 있듯이 때 ASP 합니다. NET의 역할 framework가 활성화 형식의 사용자 지정 보안 주체 개체를 만듭니다 [파트너가](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx) 폼 인증에서 만든 GenericPrincipal 개체를 덮어씁니다. 역할 프레임 워크의 API와 상호 작용 하는 주체의 IsInRole 메서드를 사용자 지정 하기 위해 수행 합니다.


에서는 되지 관련해 서 직접 역할을 사용 하 여 아직 있으므로 시점에 사용자 지정 보안 주체를 만들기 위한 해야 하는 유일한 이유 주체에 사용자 지정 IIdentity 개체에 연결할 것입니다. 4 단계에서에서 사용자의 회사 이름과 직함 특히에서 인증 티켓의 UserData 속성에서 추가 사용자 정보 저장에 대해 살펴보았습니다. 그러나 UserData 정보 되며만 인증 티켓을 통해 액세스할 수만 다음 문자열로 serialize 된 티켓의 저장 된 사용자 정보를 보려는에서는 언제 든 지 해야 UserData 속성을 구문 분석 의미 합니다.

IIdentity를 구현 하 고 속성을 CompanyName 및 제목을 포함 하는 클래스를 만들어 개발자 환경을 개선할 수 있습니다. 이런 방식으로 개발자 액세스 하는 현재 로그온된 한 사용자의 회사 이름 및 UserData 속성을 구문 분석 하는 방법을 알고 필요 없이 CompanyName 및 Title 속성을 통해 직접 제목입니다.

### <a name="creating-the-custom-identity-and-principal-classes"></a>사용자 지정 Id 및 주체 클래스 만들기

이 자습서에서는 만들겠습니다 principal 및 identity 개체 사용자 지정 앱에서\_코드 폴더입니다. 앱을 추가 하 여 시작\_폴더를 프로젝트 코드-솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, ASP.NET 폴더 추가 옵션을 선택 하 고 앱을 선택\_코드입니다. 앱\_코드 폴더는 웹 사이트에 특정 클래스 파일을 포함 하는 특수 한 ASP.NET 폴더입니다.

> [!NOTE]
> 앱\_코드 폴더는 웹 사이트 프로젝트 모델을 통해 프로젝트를 관리 하는 경우에 사용 해야 합니다. 사용 중인 경우는 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/asp.net/Aa336618.aspx), 표준 폴더를 만들고 클래스를 추가 합니다. 예를 들어, 클래스 라는 새 폴더를 추가 하 고 있는 코드를 배치 수 없습니다.


다음으로 두 개의 새 클래스 파일에 앱을 추가할\_코드 폴더, 명명 된 CustomIdentity.vb 하나 및 하나 라는 CustomPrincipal.vb 합니다.


[![CustomIdentity 및 CustomPrincipal 클래스를 프로젝트에 추가](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**그림 06**: CustomIdentity 및 CustomPrincipal 클래스를 프로젝트에 추가 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png))


CustomIdentity 클래스는 AuthenticationType, IsAuthenticated, 및 이름 속성을 정의 하는 IIdentity 인터페이스를 구현 하는 일을 담당 합니다. 이러한 필수 속성 외에도 관심이 기본 폼 인증 티켓 뿐만 아니라 사용자의 회사 이름 및 제목에 대 한 속성을 노출 합니다. CustomIdentity 클래스에 다음 코드를 입력 합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

클래스에 FormsAuthenticationTicket 멤버 변수를 포함 하는 참고 (\_티켓) 및 생성자를 통해이 티켓 정보를 제공 해야 합니다. 반환 된 id의 이름입니다;이 티켓 데이터는 CompanyName 및 Title 속성의 값을 반환 하도록 해당 UserData 속성 구문 분석 됩니다.

다음으로 CustomPrincipal 클래스를 만듭니다. CustomPrincipal 클래스의 생성자 CustomIdentity 개체만; 허용 하므로 신경쓰지 않습니다 역할과 시점에, 해당 IsInRole 메서드는 항상 False를 반환합니다.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>들어오는 요청의 보안 컨텍스트에 CustomPrincipal 개체 할당

이제 사용자 지정 id를 사용 하는 사용자 지정 보안 주체 클래스 뿐만 아니라 CompanyName 및 제목 속성을 포함 하도록 기본 IIdentity 사양을 확장 하는 클래스입니다. ASP.NET 파이프라인을 한 단계씩 실행 준비가 하 고 들어오는 요청의 보안 컨텍스트를이 사용자 지정 보안 주체 개체를 할당 합니다.

ASP.NET 파이프라인에는 들어오는 요청을 사용 하 고 여러 단계를 통해 처리 합니다. 각 단계에서 개발자가 ASP.NET 파이프라인을 활용 하 고 해당 수명 주기에서 특정 시점에 요청을 수정할 수 있으므로 특정 이벤트가 발생할 때. Formsauthenticationmodule은, 예를 들어 ASP.NET 발생에 대 한 대기를 [AuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), 인증 티켓에 대 한 들어오는 요청을 검사 하는 시점입니다. 인증 티켓 있으면 GenericPrincipal 개체를 만들고 HttpContext.User 속성에 할당 합니다.

ASP.NET 파이프라인에서 AuthenticateRequest 이벤트가 후 발생 합니다 [PostAuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)는 formsauthenticationmodule은의 인스턴스를 사용 하 여 만든 GenericPrincipal 개체를 바꿀 수 것은 CustomPrincipal 개체입니다. 그림 7에서는이 워크플로 보여 줍니다.


[![GenericPrincipal PostAuthenticationRequest 이벤트에서 CustomPrincipal으로 바뀝니다.](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**그림 07**: The GenericPrincipal PostAuthenticationRequest 이벤트에서 CustomPrincipal 바뀝니다 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png))


를 ASP.NET 파이프라인 이벤트에 대 한 응답에서 코드를 실행 하기 위해에서는 Global.asax의 적절 한 이벤트 처리기를 만듭니다 하거나 고유한 HTTP 모듈을 만듭니다. 이 자습서에 대 한 Global.asax의 이벤트 처리기를 만들어 보겠습니다. Global.asax 웹 사이트를 추가 하 여 시작 합니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 Global.asax 이라는 전역 응용 프로그램 클래스 형식의 항목을 추가 합니다.


[![Global.asax 파일을 웹 사이트 추가](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**그림 08**: 웹 사이트를 Global.asax 파일 추가 ([큰 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png))


기본 Global.asax 템플릿은 시작, 끝을 포함 하 여 ASP.NET 파이프라인 이벤트의 수에 대 한 이벤트 처리기를 포함 하 고 [오류 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx), 특히 합니다. 자유롭게에서는 필요 없는이 응용 프로그램으로 이러한 이벤트 처리기를 제거 합니다. 관심이 이벤트 PostAuthenticateRequest입니다. 태그는 다음과 비슷하게 표시 됩니다 Global.asax 파일을 업데이트 합니다.

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

응용 프로그램\_OnPostAuthenticateRequest 메서드가 실행 될 때마다 ASP.NET 런타임이 들어오는 각 페이지 요청에서 한 번 발생 하는 PostAuthenticateRequest 이벤트를 발생 시킵니다. 이벤트 처리기는 사용자가 인증 되 고 폼 인증을 통해 인증 된 경우 참조를 확인 하 여 시작 합니다. 따라서 새 CustomIdentity 개체를 만든 경우 현재 요청의 인증 티켓의 생성자에 전달 합니다. 그런 다음, CustomPrincipal 개체 만들어지고 CustomIdentity 방금 만든 개체의 생성자에 전달 합니다. 마지막으로, 현재 요청의 보안 컨텍스트는 새로 만든된 CustomPrincipal 개체에 할당 됩니다.

참고-CustomPrincipal 개체 요청의 보안 컨텍스트를 사용 하 여 연결-마지막 단계는 두 속성에 보안 주체를 매기: HttpContext.User 및 Thread.CurrentPrincipal 합니다. 이러한 두 할당은 보안 컨텍스트는 ASP.NET에서 처리 되는 방식 때문에 필요 합니다. .NET Framework는 각 실행 스레드를 사용 하 여 보안 컨텍스트 연결 이 정보를 통해 IPrincipal 개체로 사용 합니다 [스레드 개체](https://msdn.microsoft.com/library/system.threading.thread.aspx)의 [CurrentPrincipal 속성](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)합니다. 혼란은 ASP.NET에는 자체 보안 컨텍스트 정보 (HttpContext.User)입니다.

특정 시나리오에서 Thread.CurrentPrincipal 속성을 보안 컨텍스트를 결정할 때 검사 다른 시나리오에서는 HttpContext.User 사용 됩니다. 예를 들어, 개발자가 선언적으로 사용자 상태를 허용 하는.NET의 보안 기능을 가지 또는 역할 클래스를 인스턴스화할 하거나 특정 메서드를 호출할 수 있습니다 (참조 [비즈니스 및 사용 하 여 데이터 계층에 권한 부여 규칙 추가 PrincipalPermissionAttributes](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)). 내부적으로 이러한 선언적 기술을 Thread.CurrentPrincipal 속성을 통해 보안 컨텍스트를 결정 합니다.

다른 시나리오의 경우 HttpContext.User 속성을 사용 합니다. 예를 들어, 이전 자습서에서 사용 했습니다이 속성에서 현재 로그온 한 사용자의 사용자 이름을 표시 하려면. 물론 그런 다음 반드시 Thread.CurrentPrincipal 및 HttpContext.User 속성에 보안 컨텍스트 정보를 여행자 합니다.

ASP.NET 런타임은 우리 회사에 이러한 속성 값을 자동으로 동기화합니다. 그러나이 동기화 AuthenticateRequest 이벤트가 발생 한 후에 발생 하지만 *하기 전에* PostAuthenticateRequest 이벤트. 따라서 수동으로 Thread.CurrentPrincipal 그렇지 Thread.CurrentPrincipal을 할당 하려면 특정을 할 필요가 PostAuthenticateRequest 이벤트에 사용자 지정 보안 주체를 추가 하는 경우 및 HttpContext.User 동기화 됩니다. 참조 [Context.User vs. Thread.CurrentPrincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) 이 문제에 대 한 자세한 논의 합니다.

### <a name="accessing-the-companyname-and-title-properties"></a>CompanyName 및 Title 속성에 액세스

요청이 도착 하 고 ASP.NET 엔진을 응용 프로그램에 디스패치 됩니다 때마다\_Global.asax의 OnPostAuthenticateRequest 이벤트 처리기는 발생 합니다. 요청 FormsAuthenticationModule로 인증 되 면 이벤트 처리기는 폼 인증 티켓에 따라 CustomIdentity 개체를 사용 하 여 새 CustomPrincipal 개체를 만듭니다. 현재 위치에서이 논리를 사용 하 여 현재 로그온된 한 사용자의 회사 이름 및 제목에 대 한 정보에 액세스 하는 매우 간단 합니다.

페이지로 돌아가서\_Load 이벤트 처리기에서 Default.aspx 여기서 4 단계에서에서 우리가 작성 한 코드를 폼 인증 티켓을 검색 하 여 사용자의 회사 이름 및 제목 표시 하기 위해 UserData 속성을 구문 분석 합니다. 이제 사용에서 CustomPrincipal 및 CustomIdentity 개체를 사용 하 여 티켓의 UserData 속성에서 값을 구문 분석 않아도가 됩니다. 대신 단순히 CustomIdentity 개체에 대 한 참조를 가져오고 해당 CompanyName 및 제목 속성을 사용 하 여:

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>요약

이 자습서에서는 Web.config 통해 폼 인증 시스템의 설정을 사용자 지정 하는 방법을 살펴보았습니다. 인증 티켓의 만료를 처리 하는 방법 및 티켓 검사 및 수정 으로부터 보호 하기 위해 암호화 및 유효성 검사 세이프 가드를 사용 하는 방법에 대해 살펴보았습니다. 마지막으로 인증 티켓의 UserData 속성을 사용 하 여 저장할 자체 티켓의 추가 사용자 정보 및 더 개발자 친화적 방식으로이 정보를 노출 하도록 사용자 지정 principal 및 identity 개체를 사용 하는 방법을 설명 합니다.

이 자습서는 asp.net에서 폼 인증 검사를 완료 했습니다. 다음 자습서는 멤버 자격 프레임 워크에이 과정을 시작합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [폼 인증 분석](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [ASP.NET 2.0에서에서 폼 인증 설명 되어 있습니다.](https://msdn.microsoft.com/library/aa480476.aspx)
- [How To: Protect ASP.NET 2.0에서에서 폼 인증](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [보안 로그인 컨트롤](https://msdn.microsoft.com/library/ms178346.aspx)
- [합니다 &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [합니다 &lt;forms&gt; 요소에 대 한 &lt;인증&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [합니다 &lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [폼 인증 티켓 및 쿠키 이해](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목의 비디오 교육

- [폼 인증 속성을 변경 하는 방법](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [ASP.NET 응용 프로그램에서 쿠키 없는 인증 설정 및 사용 하는 방법](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 폼 로그인 재배치](../../../videos/authentication/asp-forms-login-relocation.md)
- [폼 로그인 사용자 지정 키 구성](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [인증 방법에 사용자 지정 데이터 추가](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [사용자 지정 보안 주체 개체 사용](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [이전](an-overview-of-forms-authentication-vb.md)
