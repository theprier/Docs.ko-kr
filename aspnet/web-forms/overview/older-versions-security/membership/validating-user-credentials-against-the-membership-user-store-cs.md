---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: 멤버 자격 사용자 저장소 (C#)에 대 한 사용자 자격 증명 유효성 검사 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 프로그래밍 방식으로 및 로그인 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: e0675bc814d293c6b7eff1789622158f907ebdff
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395281"
---
<a name="validating-user-credentials-against-the-membership-user-store-c"></a>멤버 자격 사용자 저장소 (C#)에 대 한 사용자 자격 증명 유효성 검사
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> 이 자습서에서는 프로그래밍 방식으로 및 로그인 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 살펴보겠습니다. Login 컨트롤의 모양 및 동작을 사용자 지정 하는 방법에도 살펴보겠습니다.


## <a name="introduction"></a>소개

에 <a id="Tutorial05"> </a> [이전 자습서](creating-user-accounts-cs.md) 멤버 자격 프레임 워크에서 새 사용자 계정을 만드는 방법에 살펴보았습니다. 먼저 사용자 계정을 통해 프로그래밍 방식으로 만드는 살펴보았습니다 합니다 `Membership` 클래스의 `CreateUser` 메서드를 CreateUserWizard 웹 컨트롤을 사용 하 여 조사 하 고 합니다. 그러나 로그인 페이지는 현재 사용자 이름 및 암호 쌍의 하드 코드 된 목록에 대해 제공된 된 자격 증명을 확인합니다. 멤버 자격 프레임 워크의 사용자 저장소에 대해 자격 증명의 유효성을 검사 하도록 로그인 페이지의 논리를 업데이트 해야 합니다.

훨씬 같은 사용자 계정을 만들고 사용 하 여 자격 증명 유효성을 검사할 수 프로그래밍 방식으로 또는 선언적으로 합니다. 멤버 자격 API를 프로그래밍 방식으로 사용자 저장소에 대 한 사용자의 자격 증명 유효성 검사에 대 한 메서드를 포함 합니다. 및 ASP.NET 사용자 이름 및 암호 로그인 단추 텍스트 상자를 사용 하 여 사용자 인터페이스를 렌더링 하는 로그인 웹 컨트롤을 포함 합니다.

이 자습서에서는 프로그래밍 방식으로 및 로그인 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 살펴보겠습니다. Login 컨트롤의 모양 및 동작을 사용자 지정 하는 방법에도 살펴보겠습니다. 이제 시작 하겠습니다.

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1 단계: 멤버 자격 사용자 저장소에 대해 자격 증명 유효성 검사

폼 인증을 사용 하는 웹 사이트에 대 한 사용자 로그온 웹 사이트에 로그인 페이지를 방문 하 여 자격 증명을 입력 합니다. 그런 다음 이러한 자격 증명 사용자 저장소에 대해 비교 됩니다. 유효한 경우에 사용자 id 및 방문자의 신뢰성이 유효한 지를 나타내는 보안 토큰을 폼 인증 티켓을 부여 됩니다.

멤버 자격 프레임 워크에 대 한 사용자의 유효성을 검사 하려면 사용 합니다 `Membership` 클래스의 [ `ValidateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)합니다. `ValidateUser` 메서드는 두 입력된 매개 변수 *`username`* 하 고 *`password`* -자격 증명이 유효한 지 여부를 나타내는 부울 값을 반환 합니다. 와 마찬가지로 합니다 `CreateUser` 이전 자습서에서는 검사할 메서드를 `ValidateUser` 실제 유효성 검사 구성된 된 멤버 자격 공급자를 위임 하는 메서드.

합니다 `SqlMembershipProvider` 제공된 된 자격 증명을 통해 지정된 된 사용자의 암호를 확보 하 여 유효성을 검사 합니다 `aspnet_Membership_GetPasswordWithFormat` 저장 프로시저입니다. 이전에 설명한 대로 `SqlMembershipProvider` 세 가지 형식 중 하나를 사용 하 여 사용자의 암호를 저장 합니다: clear, 암호화, 해시 또는 합니다. `aspnet_Membership_GetPasswordWithFormat` 원시 형식으로 저장된 프로시저에 암호를 반환 합니다. 암호화 되었거나 해시 된 암호에 대 한는 `SqlMembershipProvider` 변환를 *`password`* 에 전달 된 값을 `ValidateUser` 메서드를 해당 하는 암호화 상태를 해시 및 다음에서 반환 된 비교를 데이터베이스입니다. 데이터베이스에 저장 된 암호는 사용자가 입력 한 서식이 지정 된 암호와 일치 하는 경우 자격 증명이 잘못 되었습니다.

로그인 페이지를 업데이트 해 보겠습니다 (~ /`Login.aspx`)는 멤버 자격 프레임 워크 사용자 저장소에 대해 제공된 된 자격 증명의 유효성을 검사 합니다. 이 로그인 페이지를 만들었습니다 년대 합니다 <a id="Tutorial02"> </a> [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서에서는 사용자 이름 및 암호에 대 한 두 개의 텍스트 상자를 사용 하 여 인터페이스를 만들기는 암호 저장 확인란을 선택 하 고 로그인 단추 (그림 1 참조). 코드에 하드 코드 된 목록 (Scott/암호, Jisun/암호 및 Sam/암호) 사용자 이름 및 암호 쌍에 대해 입력 한 자격 증명을 확인합니다. 에 <a id="Tutorial03"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서의 형태로 추가 정보를 저장 하는 로그인 페이지의 코드를 업데이트 했습니다 인증 티켓의 `UserData` 속성입니다.


[![로그인 페이지의 인터페이스에 두 개의 텍스트 상자, CheckBoxList, 및 단추가 포함 됩니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**그림 1**:의 로그인 페이지의 인터페이스에 포함 되어 두 개의 텍스트 상자, CheckBoxList, 및 단추 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png))


로그인 페이지의 사용자 인터페이스 수는 변경 되지 않지만 로그인 단추를 바꾸려면 먼저 `Click` framework 멤버 자격 사용자 저장소에 대 한 사용자의 유효성을 검사 하는 코드를 사용 하 여 이벤트 처리기입니다. 해당 코드는 다음과 같이 표시 되도록 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

이 코드는 매우 간단 합니다. 호출 하 여 먼저를 `Membership.ValidateUser` 메서드를 제공 된 사용자 이름 및 암호를 전달 합니다. 통해 사이트에 사용자가 로그인 하는 경우 해당 메서드가 true를 반환 합니다 `FormsAuthentication` 클래스의 RedirectFromLoginPage 메서드. (에서 설명한 대로 합니다 <a id="Tutorial2"> </a> [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서는 `FormsAuthentication.RedirectFromLoginPage` 폼 인증 티켓을 만들고 해당 사용자를 리디렉션합니다 해당 페이지로.) 그러나 자격 증명이 유효 하지 않으면,는 `InvalidCredentialsMessage` 는 자신의 사용자 이름 또는 암호가 올바르지 않은 사용자에 게 알리는 레이블이 표시 됩니다.

이것이 전부입니다!

로그인 페이지 예상 대로 작동 하는지 테스트 하려면 이전 자습서에서 만든 사용자 계정 중 하나를 사용 하 여 로그인 하려고 합니다. 또는 계정을 아직 만들지 않은 경우 계속 해 서에서 만들는 `~/Membership/CreatingUserAccounts.aspx` 페이지입니다.

> [!NOTE]
> 암호를 포함 하 여 자격 증명을 웹 서버에 인터넷을 통해 전송 됩니다 때 사용자가 자격 증명을 입력 하 고 로그인 페이지 양식 제출 합니다 *일반 텍스트*합니다. 즉, 사용자 이름 및 암호를 네트워크 트래픽을 검사 하는 모든 해커가 볼 수 있습니다. 이 방지 하려면 반드시 사용 하 여 네트워크 트래픽을 암호화할 [보안 소켓 레이어 (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)합니다. 이렇게 하면 자격 증명 (뿐만 아니라 전체 페이지의 HTML 태그) 웹 서버에서 수신 될 때까지 브라우저를 떠날 순간부터 암호화 됩니다.


### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>멤버 자격 프레임 워크에서 잘못 된 로그인 시도 처리 하는 방법

방문자는 로그인 페이지에 도달 하 고 자격 증명을 제출, 브라우저는 로그인 페이지에 HTTP 요청을 만듭니다. 자격 증명에 유효한 경우 HTTP 응답 쿠키에서 인증 티켓을 포함 합니다. 따라서 사이트에 침투 하려고 해커가 철저히 유효한 사용자 이름 및 암호 추측을 사용 하 여 로그인 페이지에 HTTP 요청을 전송 하는 프로그램을 만들 수입니다. 암호 추측이 올바른지 로그인 페이지는이 시점에서 프로그램 알고 유효한 사용자 이름/암호 쌍으로 잘라내기와 인증 티켓 쿠키를 반환 합니다. 무차별을 통해 암호가 강력 하지 않은 경우에 특히에 이러한 프로그램을 사용자의 암호 문제는 자주 할 수 있습니다.

이러한 무차별 공격을 방지 하려면 멤버 자격 프레임 워크 특정 특정 기간 내에 실패 한 로그인 시도 수 없으면 사용자 아웃 잠급니다. 정확한 매개 변수는 다음 두 개의 멤버 자격 공급자 구성 설정을 통해 구성할 수 있습니다.

- `maxInvalidPasswordAttempts` -얼마나 많은 잘못 된 암호를 지정 합니다. 계정을 잠그기 전에 기간 내 사용자에 대해 시도할 수 있습니다. 기본값은 5입니다.
- `passwordAttemptWindow` -기간 (분) 동안 지정 된 잘못 된 로그인 시도 횟수 하면 계정이 잠길 수를 나타냅니다. 기본값은 10입니다.

사용자가 잠겨, 경우 관리자에 게 계정의 잠금을 해제 될 때까지 로그인 할 수 없습니다 그녀 합니다. 사용자가 잠겨 있는 경우는 `ValidateUser` 메서드는 *항상* 반환 `false`유효한 자격 증명이 제공 하는 경우에 합니다. 이 동작은 더 쉬워질 수 있습니다 (brute force) 메서드를 통해 사이트 해커가 끊어집니다 가능성이, 하는 동안에 단순히 암호를 잊어버렸으며 실수로 Caps Lock에 또는 잘못 된 입력 하루가 유효한 사용자를 잠그는를 종료할 수 있습니다.

그러나 사용자 계정 잠금 해제에 대 한 기본 제공 도구가 없는 합니다. 계정 잠금 해제 하기 위해 데이터베이스를 수정할 수 있습니다 직접 변경 합니다 `IsLockedOut` 필드에 `aspnet_Membership` -적절 한 사용자 계정의 테이블을 만들거나 웹 기반 인터페이스를 나열 하는 계정 잠금 해제 하는 옵션을 사용 하 여 잠긴 합니다. 이후 자습서에서 일반 사용자 계정 및 역할에 관련 된 작업을 수행 하는 것에 대 한 관리 인터페이스를 만들기를 살펴보겠습니다.

> [!NOTE]
> 단점 중 하나는 `ValidateUser` 메서드는 제공 된 자격 증명이 잘못 된 경우 제공 하지 않으며 이유에 대 한 아무런 설명 됩니다. 자격 증명에에서 있기 때문에 일치 하는 사용자 이름/암호 쌍을 없습니다 사용자 저장소 또는 사용자 아직 승인 되지 않은, 때문에 또는 사용자를 잠겨 있기 때문에 유효 하지 수 있습니다. 4 단계에서에서 해당 로그인에 실패할 경우 사용자에 게 자세한 메시지를 표시 하는 방법을 살펴보겠습니다.


## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>로그인 웹 컨트롤을 통해 자격 증명을 수집 하는 2 단계:

합니다 [로그인 웹 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) 기본 사용자 인터페이스를 다시 만든 것과 매우 비슷합니다 렌더링 합니다 <a id="SKM5"> </a> [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서. 로그인 컨트롤을 사용 하 여 방문자가 자격 증명을 수집 하는 인터페이스를 만드는 경우의 작업을 덕분입니다. 또한 로그인 컨트롤 자동으로 로그인 (제출 된 자격 증명이 잘못 가정), 사용자 함으로써 우리 저장 코드를 작성 하지 않고도 합니다.

업데이트 해 보겠습니다 `Login.aspx`를 수동으로 만든된 인터페이스를 대체 하 고 로그인 컨트롤을 사용 하 여 코딩 합니다. 기존 태그를 제거 하 여 시작 하 고 코드 `Login.aspx`합니다. 완전 한, 삭제 하거나 주석으로 처리는 단순히 있습니다. 선언적 태그를 주석으로 사용 하 여 둘러싸서 합니다 `<%--` 및 `--%>` 구분 기호입니다. 이러한 구분 기호를 수동으로 입력할 수 있습니다 또는 그림 2에서 알 수 있듯이, 주석 처리를 누른 다음 도구 모음에서 선택한 줄 아이콘 주석 텍스트를 선택할 수 있습니다. 마찬가지로, 아이콘을 선택한 줄 주석 코드 숨김 클래스에서 선택한 코드를 주석 처리를 사용할 수 있습니다.


[![선언적 태그 기존 및 Login.aspx의 소스 코드 주석](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**그림 2**: 주석 아웃은 기존 선언적 태그 및 소스 코드 `Login.aspx` ([클릭 하 여 큰 이미지 보기](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png))


> [!NOTE]
> 선택한 줄 아이콘 주석 Visual Studio 2005에서 선언적 태그를 볼 때 사용할 수 없는 경우 Visual Studio 2008을 사용 하지 않는 경우 수동으로 추가 해야 합니다는 `<%--` 고 `--%>` 구분 기호입니다.


다음으로, 로그인 컨트롤을 페이지에 도구 상자에서 끌어서 설정 해당 `ID` 속성을 `myLogin`입니다. 이 시점에서 화면 그림 3 유사 합니다. Login 컨트롤의 기본 인터페이스 이름과 암호는 암호 저장에 대 한 TextBox 컨트롤에 포함 하는 참고는 다음 확인란을 선택 하 고 로그에서 단추 시간입니다. 이 밖에도 `RequiredFieldValidator` 두 텍스트 상자에 대 한 제어 합니다.


[![로그인 컨트롤을 페이지 추가](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**그림 3**: 로그인 컨트롤을 페이지 추가 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png))


및 완료 되었습니다! Login 컨트롤의 로그인 단추를 클릭 하면 포스트백이 발생 하 고 로그인 컨트롤을 호출 하는 `Membership.ValidateUser` 메서드를 입력 한 사용자 이름 및 암호를 전달 합니다. 잘못 된 자격 증명을 로그인 컨트롤 같은 메시지가 표시 됩니다. 그러나 자격 증명이 유효 하는 경우 로그인 컨트롤 폼 인증 티켓을 만들어 및 적절 한 페이지로 사용자를 리디렉션합니다.

Login 컨트롤 네 가지 요소를 사용 하 여 로그인이 성공 하면 사용자를 리디렉션할 적절 한 페이지를 확인 하려면:

- Login 컨트롤 인지 로그인 페이지에 정의 된 대로 `loginUrl` 이 설정의 기본값은 없으며 폼 인증 구성에서 설정 `Login.aspx`
- 현재 상태를 `ReturnUrl` querystring 매개 변수
- 로그인 컨트롤의 값 [ `DestinationUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)
- `defaultUrl` 인증 구성 설정 형식에 지정 된 값이이 설정의 기본값은; `Default.aspx`

그림 4는 방법을 보여 주며 로그인 컨트롤에서 해당 페이지를 적절 한 의사 결정에 도착 하는 데 이러한 4 개의 매개 변수를 사용 합니다.


[![로그인 컨트롤을 페이지 추가](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**그림 4**: 로그인 컨트롤을 페이지 추가 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png))


브라우저를 통해 사이트를 방문 하 고 멤버 자격 프레임 워크에서 기존 사용자로 로그인 하 여 로그인 컨트롤을 테스트 하려면 잠시 시간이 소요 됩니다.

Login 컨트롤의 렌더링 된 인터페이스는 항상 구성할 수 있습니다. 다양 한 모양을;에 영향을 주는 속성 게다가 Login 컨트롤 변환할 수 있습니다 정확 하 게 제어할 레이아웃에 대 한 템플릿을 사용자 인터페이스 요소입니다. 이 단계의 나머지 모양과 레이아웃을 사용자 지정 하는 방법을 검사 합니다.

### <a name="customizing-the-login-controls-appearance"></a>Login 컨트롤의 모양 사용자 지정

Login 컨트롤의 기본 속성 설정을 제목 (로그인)를 사용 하 여 사용자 인터페이스를 렌더링, 확인란을 선택 하 고 로그인 단추에 다음 텍스트 상자 및 레이블 컨트롤을 암호 저장 사용자 이름 및 암호 입력에 대 한 시간입니다. 이러한 요소의 모양을 모든 로그인 컨트롤의 다양 한 속성을 통해 구성할 수 있습니다. 또한 새 사용자 계정 만들기-페이지에 대 한 링크와 같은 추가 사용자 인터페이스 요소-속성 또는 두 개를 설정 하 여 추가할 수 있습니다.

Gussy 우리의 로그인 컨트롤의 모양을 구성 하는 데는 몇 분 정도 소요 보겠습니다. 이후를 `Login.aspx` 페이지에 이미 로그인 라는 페이지의 맨 위에 있는 텍스트, 로그인 컨트롤의 제목은 불필요 합니다. 따라서 지울 합니다 [ `TitleText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) 로그인 컨트롤의 제목을 제거 하려면 값입니다.

사용자 이름: 및 암호: 두 TextBox 컨트롤의 왼쪽에 레이블을 통해 사용자 지정할 수 있습니다 합니다 [ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) 하 고 [ `PasswordLabelText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)각각. 이름을 변경 하 고 사용자: Username을 읽기 위한 레이블:입니다. 레이블과 텍스트 상자 스타일을 통해 구성할 수는 [ `LabelStyle` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) 하 고 [ `TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx), 각각.

기억 me 로그인 컨트롤을 통해 다음 시간 확인란의 텍스트 속성을 설정할 수 있습니다 [ `RememberMeText property` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx), 기본 확인 상태를 통해 구성할 수는 [ `RememberMeSet property` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) ( 기본값은 False)입니다. 계속 해 서 설정 된 `RememberMeSet` 속성을 다음 시간을 암호 저장 확인란 있도록 true로 기본으로 선택 됩니다.

Login 컨트롤은 해당 사용자 인터페이스 컨트롤의 레이아웃을 조정 하는 것에 대 한 두 가지 속성을 제공 합니다. 합니다 [ `TextLayout property` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) 나타냅니다 여부를 사용자 이름: 및 암호:가 해당 텍스트 상자 (기본값) 또는 상위 왼쪽에 레이블을 표시 합니다. 합니다 [ `Orientation property` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) 사용자 이름 및 암호 입력 세로로 배치 하는지 여부를 나타냅니다 (위와 다른) 또는 수평으로 합니다. 이러한 두 속성을 기본값으로 설정 유지 하려고 하지만 결과 효과 확인 하려면 기본이 아닌 값으로 이러한 두 속성을 설정 하려는 것이 좋습니다.

> [!NOTE]
> 다음 섹션에서는 로그인 컨트롤의 레이아웃을 구성 살펴보겠습니다 템플릿을 사용 하 여 레이아웃 컨트롤의 사용자 인터페이스 요소의 정확한 레이아웃을 정의 합니다.


Login 컨트롤의 속성 설정을 설정 하 여 마무리 합니다 [ `CreateUserText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) 및 [ `CreateUserUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) 아직 등록 되지 않음에? 계정 만들기 및 `~/Membership/CreatingUserAccounts.aspx`, 각각. 만든 Login 컨트롤의 인터페이스는 페이지를 가리키는 하이퍼링크를 추가 합니다 <a id="SKM6"> </a> [이전 자습서](creating-user-accounts-cs.md)합니다. Login 컨트롤의 [ `HelpPageText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) 하 고 [ `HelpPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) 및 [ `PasswordRecoveryText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) 하 고 [ `PasswordRecoveryUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) 도움말 페이지 및 암호 복구 페이지에 대 한 링크를 렌더링 하 동일한 방식으로 작동 합니다.

속성을 변경한 후 로그인 컨트롤의 선언적 태그 및 모양을 유사 그림 5에 표시 된 것입니다.


[![Login 컨트롤의 속성 값의 모양을 지정합니다](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**그림 5**: The 로그인 컨트롤의 속성 값 결정 해당 모양 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png))


### <a name="configuring-the-login-controls-layout"></a>Login 컨트롤의 레이아웃을 구성합니다.

로그인 웹 컨트롤의 기본 사용자 인터페이스는 html에서 인터페이스 레이아웃 `<table>`합니다. 그러나 렌더링 된 출력을 보다 세부적으로 제어 해야 될까요? 으로 대체 합니다 `<table>` 일련의 `<div>` 태그입니다. 또는 응용 프로그램 인증에 대 한 추가 자격 증명을 요구 하는 경우에 어떨까요? 많은 재무 웹 사이트에는 예를 들어 뿐 아니라 사용자 이름 및 암호를 하지만 또한을 개인 식별 번호 (PIN), 또는 기타 식별 정보를 입력 하 게 필요 합니다. 어떤 이유 수, 로그인 컨트롤을 정의할 수 있습니다 명시적으로 인터페이스를 선언적 태그 템플릿으로 변환할 가능성이 있습니다.

추가 자격 증명을 수집 하려면 로그인 컨트롤을 업데이트 하기 위해 두 가지를 수행 해야 합니다.

1. 추가 자격 증명을 수집 하려면 웹 컨트롤을 포함 하도록 로그인 컨트롤의 인터페이스를 업데이트 합니다.
2. 사용자가 사용자 이름과 암호가 유효 하 고 추가 자격 증명도 유효한 경우에 인증 됩니다 있도록 로그인 컨트롤의 내부 인증 논리를 재정의 합니다.

첫 번째 작업을 수행 하려면 Login 컨트롤 템플릿으로 변환 하 고 필요한 웹 컨트롤을 추가 해야 합니다. 두 번째 작업의 경우 Login 컨트롤의 인증 논리 대체 될 수 있습니다 컨트롤에 대 한 이벤트 처리기를 만들어 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)합니다.

자신의 사용자 이름, 암호 및 전자 메일 주소에 대 한 메시지를 표시 하 고 제공 된 전자 메일 주소가 파일에서 전자 메일 주소와 일치 하는 경우에 사용자를 인증 있도록 Login 컨트롤을 업데이트 해 보겠습니다. 먼저 로그인 컨트롤의 인터페이스를 템플릿으로 변환 해야 합니다. Login 컨트롤의 스마트 태그에서 템플릿 옵션으로 선택 합니다.


[![Login 컨트롤 템플릿으로 변환](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**그림 6**: Login 컨트롤 템플릿으로 변환 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png))


> [!NOTE]
> Login 컨트롤 미리 template 버전으로 되돌리려면 컨트롤의 스마트 태그에서 다시 설정 링크를 클릭 합니다.


추가 로그인 컨트롤을 템플릿으로 변환는 `LayoutTemplate` HTML 요소 및 사용자 인터페이스를 정의 하는 웹 컨트롤을 사용 하 여 컨트롤의 선언적 태그를 합니다. 그림 7에서 알 수 있듯이, 컨트롤을 템플릿으로 변환 제거 다양 한 속성이 속성 창에서와 같은 `TitleText`, `CreateUserUrl`등, 있으므로 템플릿을 사용 하는 경우 이러한 속성 값은 무시 됩니다.


[![적은 수의 속성은 사용할 수 있는 경우는 로그인 컨트롤 템플릿으로 변환 하는](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**그림 7**: 적은 수의 속성은 사용할 수 있는 경우는 로그인 컨트롤 템플릿으로 변환 됩니다 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png))


HTML 태그를 `LayoutTemplate` 필요에 따라 수정할 수 있습니다. 마찬가지로, 언제 든 지 새 웹 컨트롤 템플릿에 추가 합니다. 그러나 반드시 해당 로그인 컨트롤의 핵심 웹 컨트롤 서식 파일에 남아 있으며 할당 된 유지 `ID` 값입니다. 특히 제거 하거나 마십시오 이름 바꾸기는 `UserName` 또는 `Password` 텍스트 상자를 `RememberMe` 확인란을를 `LoginButton` 단추를 `FailureText` 레이블을 또는 `RequiredFieldValidator` 컨트롤.

방문자의 전자 메일 주소를 수집 하려면 템플릿에 TextBox를 추가 해야 합니다. 테이블 행 간의 다음 선언적 태그를 추가 (`<tr>`)를 포함 하는 `Password` 텍스트 상자 및 암호 저장 다음 보유 하는 테이블 행 확인란 시간:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

추가한 후의 `Email` 텍스트 상자에 브라우저를 통해 페이지를 방문 합니다. 그림 8에서 알 수 있듯이, 로그인 컨트롤의 사용자 인터페이스는 이제 세 번째 텍스트 상자를 포함 합니다.


[![Login 컨트롤 이제 사용자의 전자 메일 주소에 대 한 텍스트를 포함](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**그림 8**: Login 컨트롤 이제 사용자의 전자 메일 주소에 대 한 텍스트를 포함 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png))


Login 컨트롤이 시점에서 여전히 사용 하 여 `Membership.ValidateUser` 제공된 된 자격 증명의 유효성을 검사 하는 방법입니다. 마찬가지로, 값을 입력 합니다 `Email` 텍스트 상자에 사용자 로그인 할 수 있는지 여부에 관여 하지 않습니다. 3 단계에서에서 자격 증명은만 유효 사용자 이름 및 암호 유효 하 고 제공 된 전자 메일 주소 파일에서 전자 메일 주소와 일치 하는 경우 수 있도록 로그인 컨트롤의 인증 논리를 재정의 하는 방법을 살펴보겠습니다.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3 단계: 로그인 컨트롤의 인증 논리를 수정합니다.

그녀는 방문자가 제공 하는 경우 로그인 자격 증명 및 로그인 단추를 다시 게시 근거가 번의 클릭 만으로 인증 워크플로 진행을 제어 합니다. 시켜 워크플로 시작 합니다 [ `LoggingIn` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)합니다. 이 이벤트와 연결 된 모든 이벤트 처리기를 설정 하 여 작업에 대 한 로그인을 취소할 수는 `e.Cancel` 속성을 `true`입니다.

시켜 워크플로 진행 중인 작업의 로그를 취소 하지 않으면 경우는 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)합니다. 경우에 대 한 이벤트 처리기는 `Authenticate` 이벤트,이 제공 된 자격 증명이 유효한 지 여부를 결정 합니다. 이벤트 처리기를 지정 하는 경우 로그인 컨트롤에 사용 된 `Membership.ValidateUser` 자격 증명의 유효성을 검사 하는 방법입니다.

제공 된 자격 증명이 유효한 경우 폼 인증 티켓이 만들어지면 합니다 [ `LoggedIn` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) 발생 및 적절 한 페이지로 리디렉션됩니다. 그러나 자격 증명은 잘못 된 경우 간주 하는 경우 해당 [ `LoginError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) 발생 하는 자격 증명 잘못 된 사용자에 게 알리는 메시지가 표시 됩니다. 기본적으로 로그인 실패 시 컨트롤 간단히 설정 해당 `FailureText` (로그인 시도 하지 못했습니다 오류 메시지를 컨트롤의 텍스트 속성 레이블. 다시 시도 하세요). 그러나 경우 로그인 컨트롤의 [ `FailureAction` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) 로 설정 되어 `RedirectToLoginPage`, 다음 로그인 컨트롤 문제를 `Response.Redirect` querystring 매개 변수를 추가 하는 로그인 페이지로 `loginfailure=1` (그러면 로그인 오류 메시지를 표시할 컨트롤)입니다.

그림 9에서는 인증 워크플로 순서도 제공합니다.


[![Login 컨트롤의 인증 워크플로](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**그림 9**: The 로그인 컨트롤의 인증 워크플로 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png))


> [!NOTE]
> 사용 시기에 있는지를 `FailureAction`의 `RedirectToLogin` 옵션 페이지, 다음 시나리오를 고려 합니다. 지금 우리 `Site.master` 마스터 페이지에는 현재, Hello, 군에 표시할 텍스트를 익명 사용자가 방문 하는 경우 왼쪽된 열에 있지만 로그인 컨트롤을 사용 하 여 해당 텍스트를 대체 하 려 한다고 가정 합니다. 이렇게 하면 익명 사용자 로그인 페이지를 직접 방문할 필요 없이 사이트의 모든 페이지에서 로그인 합니다. 그러나 사용자는 마스터 페이지에서 렌더링 하는 로그인 컨트롤을 통해 로그인 할 수 없는 경우, 해야 로그인 페이지로 리디렉션합니다 (`Login.aspx`) 추가 지침, 링크 및 만들기에 대 한 링크와 같은 다른 도움말-가능성이 해당 페이지에 포함 되어 있으므로 새 계정 또는 마스터 페이지에 추가 되지 않은 암호가 손실된 검색 합니다.


### <a name="creating-theauthenticateevent-handler"></a>만들기는`Authenticate`이벤트 처리기

이 사용자 지정 인증 논리를 연결 하기 위해 Login 컨트롤의 이벤트 처리기를 생성 해야 `Authenticate` 이벤트입니다. 에 대 한 이벤트 처리기 만들기는 `Authenticate` 이벤트는 다음 이벤트 처리기 정의 생성 합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

알 수 있듯이 합니다 `Authenticate` 이벤트 처리기가 형식의 개체를 전달 [ `AuthenticateEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) 두 번째 입력된 매개 변수로 합니다. 합니다 `AuthenticateEventArgs` 라는 부울 속성을 포함 하는 클래스 `Authenticated` 제공 된 자격 증명이 유효한 지 여부를 지정 하는 데 사용 되는 합니다. 우리의 작업, 제공 된 자격 증명이 유효한 지 여부를 결정 하는 코드를 작성 하 고 설정 하려면 그런 다음이 `e.Authenticate` 속성 적절 하 게 합니다.

### <a name="determining-and-validating-the-supplied-credentials"></a>확인 하 고 제공 된 자격 증명 유효성 검사

로그인 컨트롤을 사용 하 여 [ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) 하 고 [ `Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) 사용자가 입력 한 사용자 이름 및 암호 자격 증명을 확인 하려면. 추가 웹 컨트롤에 입력 된 값을 확인 하기 위해 (같은 합니다 `Email` 이전 단계에서 추가한 텍스트 상자)를 사용 하 여 *`LoginControlID`* `.FindControl`("*`controlID`*")를 가져올 프로그래밍에 대 한 참조 웹 컨트롤 템플릿에 해당 `ID` 속성과 같으면 *`controlID`* 합니다. 예를 들어에 대 한 참조를 가져오려면는 `Email` 텍스트 상자에 다음 코드를 사용:

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

사용자의 자격 증명의 유효성을 검사 하기 위해 두 가지를 수행 해야 합니다.

1. 제공 된 사용자 이름과 암호가 유효한 지 확인
2. 전자 메일 주소를 입력 한 로그인을 시도 하는 사용자에 대 한 파일의 전자 메일 주소와 일치 하는지 확인

단순히 사용 하 여 첫 번째 검사를 수행 하는 `Membership.ValidateUser` 1 단계에서에서 본 것 처럼 메서드. 두 번째 확인에 대 한 것은 TextBox 컨트롤에 입력 한 전자 메일 주소로 비교할 수 있도록 사용자의 전자 메일 주소를 확인 해야 합니다. 특정 사용자에 대 한 정보를 사용 합니다 `Membership` 클래스의 [ `GetUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)합니다.

`GetUser` 메서드가 오버 로드의 수입니다. 매개 변수를 전달 하지 않고 사용 하는 경우 현재 로그인된 한 사용자에 대 한 정보를 반환 합니다. 특정 사용자에 대 한 정보를 얻으려면 호출 `GetUser` 자신의 사용자 이름을 전달 합니다. 어느 `GetUser` 반환을 [ `MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), 같은 속성이 있는 `UserName`를 `Email`, `IsApproved`, `IsOnline`등.

다음 코드는이 두 가지 검사를 구현합니다. 다음 모두 전달 하는 경우 `e.Authenticate` 로 설정 된 `true`, 그렇지 않으면 할당 `false`합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

이 코드를 사용 하 여 올바른 사용자 이름, 암호 및 전자 메일 주소를 입력 합니다. 유효한 사용자로 로그인 하려고 합니다. 이 작업을 다시 시도 하지만이 이번에는 의도적으로 잘못 된 전자 메일 주소 사용 (그림 10 참조). 마지막으로, 존재 하지 않는 사용자를 사용 하 여 세 번째로 보세요. 첫 번째 경우에서는 성공적으로 로그온 사이트로 하지만 마지막 두 경우에서 로그인 컨트롤의 잘못 된 자격 증명 메시지 표시 되어야 합니다.


[![잘못 된 전자 메일 주소를 제공 하는 경우 Tito 로그인 할 수 없습니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**그림 10**: Tito 없습니다 로그의 경우 잘못 된 전자 메일 주소를 제공 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png))


> [!NOTE]
> 1 단계에서에서 하는 방법의 멤버 자격 프레임 워크 처리 잘못 된 로그인 시도 섹션에서 설명한 대로 때는 `Membership.ValidateUser` 잘못 된 로그인 시도 추적에 특정 초과 하는 경우에 사용자를 잠그는 메서드 호출 되 고 잘못 된 자격 증명 전달 지정된 된 시간 창 내에서 잘못 된 시도 횟수의 임계값입니다. 사용자 지정 인증 논리 호출 이후에 `ValidateUser` 메서드를 올바른 사용자 이름에 잘못 된 암호를 잘못 된 로그인 시도 카운터를 하나씩 늘립니다 있지만이 카운터는 사용자 이름 및 암호는 유효한 경우에서 증가 하지 않지만 전자 메일 주소가 올바르지 않습니다. 그럴 경우이 동작은 적합 가능성이 해커는 사용자 이름과 암호를 알지만 무작위 기술을 사용 하 여 사용자의 전자 메일 주소를 확인할 필요가 없기 때문입니다.


## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4 단계: 로그인 컨트롤의 잘못 된 자격 증명 메시지 개선

사용자가 잘못 된 자격 증명을 사용 하 여 로그온 하려고 하면 로그인 컨트롤 로그인 시도가 성공 했음을 설명 하는 메시지를 표시 합니다. 컨트롤에서 지정한 메시지를 표시 하는 특히 해당 [ `FailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)에 기본값이 로그인 시도 실패 했습니다. 다시 시도하세요.

회수는 여러 가지 이유가 있습니다 이유는 사용자의 자격 증명이 올바르지 않을 수 있습니다.

- 사용자 이름이 없을 수 있습니다.
- 사용자 이름이 존재 하지만 암호가 올바르지 않습니다.
- Username 및 password는 유효 하지만 사용자가 아직 승인 되지 않았습니다.
- Username 및 password는 유효 하지만 사용자가 잠겨 아웃 (가장 가능성이 높은 특정된 시간 프레임 내에서 잘못 된 로그인 시도 횟수를 초과 했기 때문에)

및 다른 이유가 있을 때 사용자 지정 인증 논리를 사용 합니다. 예를 들어 코드를 사용 하 여 우리가 작성 한 3 단계에서는 사용자 이름 및 암호가 유효한 지, 것일 수 있지만 전자 메일 주소가 올바르지 않을 합니다.

이유는 자격 증명이 올바르지 않습니다에 관계 없이 로그인 컨트롤에는 동일한 오류 메시지가 표시 됩니다. 피드백이이 부족 하다는 잠긴 계정이 아직 승인 되지 않은 사용자에 대 한 혼동 될 수 있습니다. 약간의 작업을 사용 하 여 그러나 있다는 Login 컨트롤 보다 적절 한 메시지를 표시 합니다.

사용자가 로그인 컨트롤에서 발생 하는 잘못 된 자격 증명을 사용 하 여 로그인 하려고 할 때마다 해당 `LoginError` 이벤트입니다. 계속 해 서 및이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

로그인 컨트롤을 설정 하 여 시작 하는 위의 코드 `FailureText` 속성을 기본값 (로그인 시도 하지 못했습니다. 다시 시도 하세요). 다음 확인 하 되는 경우 제공한 사용자 이름이 기존 사용자 계정에 매핑됩니다. 결과 검토를 하는 경우 `MembershipUser` 개체의 `IsLockedOut` 및 `IsApproved` 계정이 잠겼습니다 또는 아직 승인 되지 않은 경우를 결정 하는 속성입니다. 두 경우 모두를 `FailureText` 속성이 해당 값으로 업데이트 됩니다.

이 코드를 테스트 하려면 기존 사용자로 로그인 하는 잘못 된 암호를 사용 하 여 의도적으로 시도 합니다. 10 분 시간 프레임 내에서 행이 5 번 수행 하 고 계정이 잠기게 됩니다. 그림 11에서는, 후속 로그인 시도 항상 (정확한 암호 대신)으로 실패 하지 않지만 이제 더 설명적인 표시 너무 많은 잘못 된 로그인 시도 인해 계정의 잠 궜 습니다. 계정 잠금 해제 된 메시지를 포함 하도록 관리자에 게 문의 하십시오.


[![Tito 너무 많은 잘못 된 로그인 시도 수행 하 고이 잠겨](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**그림 11**:가 된 잠겨 Tito 수행 너무 많은 잘못 된 로그인 시도 하 고 ([큰 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png))


## <a name="summary"></a>요약

이전이 자습서에서는 로그인 페이지 사용자 이름/암호 쌍의 하드 코드 된 목록에 대해 제공된 된 자격 증명의 유효성을 검사 합니다. 이 자습서에서는 멤버 자격 프레임 워크에 대해 자격 증명의 유효성을 검사 하려면 페이지를 업데이트 했습니다. 1 단계에서에서 사용 하 여 살펴보았습니다는 `Membership.ValidateUser` 메서드 프로그래밍 방식으로 합니다. 2 단계에서에서 교체는 수동으로 만든된 사용자 인터페이스 및 코드 로그인 컨트롤을 사용 하 여 합니다.

Login 컨트롤 표준 로그인 사용자 인터페이스를 렌더링 하 고 자동으로 멤버 자격 프레임 워크에 대 한 사용자의 자격 증명의 유효성을 검사 합니다. 또한 유효한 자격 증명을 발생 시 로그인 컨트롤 사용자를 로그인 폼 인증을 통해. 즉, 모든 기능을 갖춘 로그인 사용자 경험을은 페이지, 추가 선언적 태그 또는 코드에 필요한 로그인 컨트롤을 끌어 놓으면 하십시오. 게다가 로그인 컨트롤은 고도로 사용자 지정을 정밀 하 게 렌더링 된 사용자 인터페이스 및 인증 논리를 모두 제어할 수 있습니다.

이 시점에서 방문자가 웹 사이트를 만들 수 있습니다 새 사용자 계정 및 로그를 사이트에 있지만 인증 된 사용자를 기반으로 하는 페이지에 대 한 액세스를 제한 살펴볼 아직 있습니다. 현재 사용자, 인증 또는 익명으로 사이트의 페이지를 볼 수 있습니다. 사용자가 사용자 단위로 사이트의 페이지에 대 한 액세스 제어와 함께 특정 페이지를 사용자에 해당 기능에 따라 달라 집니다 있을 수 있습니다. 다음 자습서 권한과 로그인된 한 사용자를 기반으로 하는 페이지에서 기능을 제한 하는 방법에 살펴봅니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [잠긴 및 승인 되지 않은 사용자는 사용자 지정 메시지를 표시 합니다.](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 로그인 페이지를 만듭니다.](https://msdn.microsoft.com/library/ms178331.aspx)
- [로그인 컨트롤에 대 한 기술 설명서](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [로그인 컨트롤을 사용 하 여](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 Michael Olivero 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [이전](creating-user-accounts-cs.md)
> [다음](user-based-authorization-cs.md)
