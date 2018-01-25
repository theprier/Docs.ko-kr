---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: "(VB)의 멤버 자격 사용자 저장소에 대 한 사용자 자격 증명 유효성 검사 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 프로그래밍 방식으로 Login 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 검토 합니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: f57bc8c32757c1ea25bf6bbb34539570e4c09aad
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="validating-user-credentials-against-the-membership-user-store-vb"></a>(VB)의 멤버 자격 사용자 저장소에 대 한 사용자 자격 증명 유효성 검사
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> 이 자습서에서는 프로그래밍 방식으로 Login 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 살펴보겠습니다. 로그인 컨트롤의 모양 및 동작을 사용자 지정 하는 방법에도 살펴보겠습니다.


## <a name="introduction"></a>소개

에 <a id="Tutorial05"> </a> [이전 자습서](creating-user-accounts-vb.md) 구성원 프레임 워크에서 새 사용자 계정을 만드는 방법을 살펴보았습니다. 먼저 프로그래밍 방식으로 작성을 통해 사용자 계정을 살펴보았습니다는 `Membership` 클래스의 `CreateUser` 메서드를 다음 CreateUserWizard 웹 컨트롤을 사용 하 여를 검사 하 고 있습니다. 그러나 로그인 페이지는 현재 사용자 이름 및 암호 쌍의 하드 코드 된 목록에 대해 제공 된 자격 증명을 확인합니다. 멤버 자격 프레임 워크의 사용자 저장소에 대 한 자격 증명의 유효성을 검사 하는 로그인 페이지의 논리를 업데이트 해야 합니다.

훨씬와 같은 사용자 계정 생성 된 자격 증명 유효성을 검사할 수 프로그래밍 방식으로 또는 선언적으로 합니다. 멤버 API는 프로그래밍 방식으로 사용자 저장소에 대 한 사용자의 자격 증명 유효성 검사에 대 한 메서드를 포함 합니다. 및 ASP.NET에는 사용자 이름 및 암호 로그인 단추 텍스트 상자는 사용자 인터페이스를 렌더링 하는 로그인 웹 컨트롤을 제공 합니다.

이 자습서에서는 프로그래밍 방식으로 Login 컨트롤을 사용 하 여 멤버 자격 사용자 저장소에 대 한 사용자의 자격 증명의 유효성을 검사 하는 방법을 살펴보겠습니다. 로그인 컨트롤의 모양 및 동작을 사용자 지정 하는 방법에도 살펴보겠습니다. 이제 시작 하겠습니다.

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1 단계: 멤버 자격 사용자 저장소에 대해 자격 증명 유효성 검사

폼 인증을 사용 하는 웹 사이트에 대 한 사용자 로그온 웹 사이트에 로그인 페이지를 방문 하 고 자격 증명을 입력 합니다. 이러한 자격 증명 사용자 저장소에 대 한 다음 비교 됩니다. 유효한 경우에 사용자 id 및 방문자의 신뢰성을 나타내는 보안 토큰을 폼 인증 티켓을 부여 됩니다.

멤버 자격 프레임 워크에 대해 사용자 확인을 위해 사용 하 여는 `Membership` 클래스의 [ `ValidateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)합니다. `ValidateUser` 메서드는 두 입력된 매개 변수- `username` 및 `password` -자격 증명이 유효한 지 여부를 나타내는 부울 값을 반환 합니다. 와 함께 `CreateUser` 에서 이전 자습서 인 검사 했습니다 메서드는 `ValidateUser` 메서드 실제 유효성 검사 구성 된 멤버 자격 공급자를 위임 합니다.

`SqlMembershipProvider` 제공 된 자격 증명을 통해 지정된 된 사용자의 암호를 확보 하 여 유효성을 검사는 `aspnet_Membership_GetPasswordWithFormat` 저장 프로시저입니다. 이전에 설명한 대로 `SqlMembershipProvider` 세 가지 형식 중 하나를 사용 하 여 사용자의 암호: 암호화, 해시 또는 선택 취소 합니다. `aspnet_Membership_GetPasswordWithFormat` 저장된 프로시저는 원시 형식으로 암호를 반환 합니다. 암호화 / 해시 된 암호에 대 한는 `SqlMembershipProvider` 변환는 `password` 에 전달 된 값은 `ValidateUser` 에 해당 하는 메서드 암호화 또는 해시 상태와 다음 데이터베이스에서 반환 된 비교 합니다. 사용자가 입력 한 서식이 지정 된 암호와 일치 하는 데이터베이스에 저장 된 암호 자격 증명이 유효 합니다.

로그인 페이지 정보를 업데이트 (~ /`Login.aspx`) 구성원 프레임 워크 사용자 저장소에 대해 제공된 된 자격 증명 유효성을 검사할 수 있도록 합니다. 만든이 로그인 페이지에 다시는 <a id="Tutorial02"> </a> [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서에서는 사용자 이름 및 암호를 두 개의 텍스트 상자를 사용 하 여 인터페이스를 만들기는 암호 저장 확인란을 선택 하 고 로그인 단추 (그림 1 참조). 코드의 하드 코드 된 목록 (Scott/암호, Jisun/암호 및 Sam/암호) 사용자 이름 및 암호 쌍에 대해 입력 한 자격 증명 유효성을 검사 합니다. 에 <a id="Tutorial03"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 자습서는 폼에 추가 정보를 저장 하는 로그인 페이지의 코드를 업데이트 했습니다. 인증 티켓 `UserData` 속성입니다.


[![두 텍스트 상자는 CheckBoxList 및 단추를 포함 하는 로그인 페이지의 인터페이스](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**그림 1**: The 로그인 페이지의 인터페이스에 포함 되어 두 개의 텍스트 상자는 CheckBoxList 및 단추 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png))


로그인 페이지의 사용자 인터페이스가 동일할 수 있지만 이러한 로그인 단추를 교체할 수 `Click` 구성원 프레임 워크 사용자 저장소에 대 한 사용자의 유효성을 검사 하는 코드와 이벤트 처리기입니다. 해당 코드가 다음과 같이 표시 되도록 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

이 코드는 매우 간단 합니다. 호출 하 여 시작 된 `Membership.ValidateUser` 메서드를 제공 된 사용자 이름 및 암호를 전달 합니다. 해당 메서드가 True를 반환 하는 경우 다음 사용자가을 통해 사이트에 로그인 된 `FormsAuthentication` 클래스의 RedirectFromLoginPage 메서드. (에서 설명한 것 처럼는 <a id="Tutorial02"> </a> [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서는 `FormsAuthentication.RedirectFromLoginPage` 폼 인증 티켓을 만들고 다음 사용자를 리디렉션합니다 적절 한 페이지로.) 그러나 자격 증명이 잘못 된 경우,는 `InvalidCredentialsMessage` 자신의 사용자 이름 또는 암호가 잘못 되었음을 사용자에 게 알리는 레이블이 표시 됩니다.

그을 마쳤습니다.

를 로그인 페이지 예상 대로 작동 하는지 테스트 하려면 이전 자습서에서 만든 사용자 계정 중 하나가 지정 된 로그인을 시도 합니다. 또는 계정을 아직 만들지 않은 경우 계속 진행 하 고에서 하나를 만들는 `~/Membership/CreatingUserAccounts.aspx` 페이지.

> [!NOTE]
> 사용자는 자신의 자격 증명을 입력 하 고 로그인 페이지 양식 제출, 암호를 포함 하 여 자격 증명을 웹 서버에 인터넷을 통해 전송 됩니다 *일반 텍스트*합니다. 즉, 네트워크 트래픽을 검사 하는 모든 해커가 사용자 이름 및 암호를 볼 수 있습니다. 이 방지 하려면 사용 하 여 네트워크 트래픽을 암호화 하는 데 필수적인은 [레이어 SSL (Secure Socket)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)합니다. 이렇게 하면 자격 증명 (뿐만 아니라 전체 페이지의 HTML 태그) 웹 서버에서 수신 될 때까지 브라우저를 남깁니다 순간부터 암호화 됩니다.


### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>멤버 자격 프레임 워크에서 잘못 된 로그인 시도 처리 하는 방법

방문자의 로그인 페이지에 도달 하 고 자격 증명을 제출, 브라우저 로그인 페이지에 HTTP 요청을 보냅니다. 자격 증명이 유효 하는 경우 HTTP 응답 쿠키에 인증 티켓을 포함 합니다. 따라서 사이트에 침입을 시도 하는 해커가 거쳤으며의 유효한 사용자 이름 및 암호에는 추측 로그인 페이지에 HTTP 요청을 전송 하는 프로그램을 만들어 합니다. 암호 추측이 올바른지 로그인 페이지는 프로그램이 시점에서 유효 사용자 이름/암호 쌍에 우연히가 알고 인증 티켓 쿠키를 반환 합니다. 무차별 암호 대입을 통해 이러한 프로그램 할 수는 사용자의 암호를 시 혼 미 마법 암호가 강력 하지 않은 경우에 특히 합니다.

이러한 무차별 암호 대입 공격을 방지 하려면 멤버 자격 프레임 워크도 잠그는 사용자 특정 특정 기간 내에 실패 한 로그인 시도 수 없는 경우. 정확한 매개 변수는 다음 두 개의 멤버 자격 공급자 구성 설정을 통해 구성할 수 없습니다.

- `maxInvalidPasswordAttempts`-잘못 된 암호 수를 지정 합니다. 계정이 잠겨 하기 전 까지의 기간 안에 시도 사용자에 대해 사용할 수 있습니다. 기본값은 5입니다.
- `passwordAttemptWindow`-는 지정 된 잘못 된 로그인 시도 횟수 하면 계정이 잠길 수 분에서 기간을 나타냅니다. 기본값은 10입니다.

사용자가 잠긴, 하는 경우 관리자가 자신의 계정을 잠금 해제할 때까지 로그인 할 수 없는 그녀 합니다. 사용자가 잠겨 있는 경우는 `ValidateUser` 방법은 *항상* 반환 `False`유효한 자격 증명을 제공 하는 경우에 합니다. 이 동작은 더 쉬워질 수 있습니다 가능성을 무작위 메서드를 통해 사이트에는 해커가 끊긴다는, 하는 동안 사용자가 암호를 잊어버렸으며 단순히 또는 실수로 Caps Lock 잘못 된 입력 일 필요는 유효한 사용자를 잠그는를 종료할 수 있습니다.

그러나 사용자 계정 잠금을 해제 하기 위한 기본 제공 도구가 없는 합니다. 계정 잠금 해제 하기 위해 데이터베이스를 수정할 수 있습니다 직접-변경할는 `IsLockedOut` 필드에 `aspnet_Membership` -적절 한 사용자 계정에 대 한 테이블을 만들거나 웹 기반 인터페이스를 나열 하는 계정 잠금 해제 하려면 옵션과 함께 잠겨 있습니다. 이후 자습서에서 일반적인 사용자 계정 및 역할 관련 작업을 수행 하기 위한 관리 인터페이스를 만들기를 검사 합니다.

> [!NOTE]
> 단점 중 하나는 `ValidateUser` 메서드는 제공 된 자격 증명이 유효 하지 않은 경우 제공 하지 않으며 이유에 대해 모든 설명을 합니다. 자격 증명 사용자 저장소에 없는 일치 하는 사용자 이름/암호 쌍이 있기 때문에 사용자 아직 승인 되지 않은 아니면 사용자가 잠긴 때문에 유효 하지 않습니다 수 있습니다. 4 단계에서에서 해당 로그인 시도가 실패할 때 사용자에 게 보다 자세한 메시지를 표시 하는 방법을 살펴봅니다.


## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>로그인 웹 컨트롤을 통해 자격 증명을 수집 하는 2 단계:

[로그인 웹 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) 기본 사용자 인터페이스를 다시에서 만든 것과 매우 비슷한 렌더링는 <a id="Tutorial02"> </a> [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서입니다. Login 컨트롤을 사용 하 여의 방문자의 자격 증명을 수집 하는 인터페이스를 만드는 작업을 저장 주세요. 또한 Login 컨트롤 자동으로 로그인 (전송 된 자격 증명이 유효 가정), 사용자 함으로써 우리 저장 코드를 작성 하지 않아도 합니다.

정보를 업데이트 `Login.aspx`, 대체 수동으로 만든된 인터페이스 및 로그인 제어를 사용한 코드입니다. 기존 태그를 제거 하 여 시작 하 고 코드에서 `Login.aspx`합니다. 완전 한, 삭제 또는 단순히 주석으로 처리 될 수 있습니다. 선언적 태그, 주석 처리를 사용 하 여 서라운드는 `<%--` 및 `--%>` 구분 기호입니다. 이러한 구분 기호를 직접 입력 또는 텍스트를 주석으로 처리 하 고 도구 모음에서 선택한 줄 아이콘 주석 클릭 그림 2에서 볼 수 있듯이 선택할 수 있습니다. 마찬가지로, 선택한 줄 아이콘 주석 코드 숨김 클래스의 선택 된 코드를 주석 처리를 사용할 수 있습니다.


[![기존 선언 태그 및 Login.aspx의 소스 코드 주석](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**그림 2**: 주석 아웃 the 기존 선언 태그 및 Login.aspx의 소스 코드 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png))


> [!NOTE]
> Visual Studio 2005에서 선언적 태그를 볼 때 선택한 줄 아이콘 주석 ´ ù. Visual Studio 2008을 사용 하지 않는 경우 수동으로 추가 해야 합니다는 `<%--` 및 `--%>` 구분 기호입니다.


다음으로, 도구 상자 페이지에서에서 로그인 컨트롤을 끌어 하 고 설정의 `ID` 속성을 `myLogin`합니다. 이 시점에서 화면 그림 3 비슷해야 합니다. 확인란과 단추에 로그에 다음 참고에 로그인 컨트롤의 기본 인터페이스에서 사용자 이름과 암호는 암호 저장에 대 한 TextBox 컨트롤이 포함 됩니다 때 합니다. 또한 `RequiredFieldValidator` 두 텍스트 상자에 대 한 제어 합니다.


[![페이지에 로그인 컨트롤 추가](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**그림 3**: 페이지에 로그인 컨트롤을 추가 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png))


완료 하 고! Login 컨트롤 로그인 단추를 클릭할 때 포스트백이 발생 하 고 Login 컨트롤 호출 됩니다는 `Membership.ValidateUser` 메서드를 입력 한 사용자 이름 및 암호를 전달 합니다. 자격 증명이 잘못 된 로그인 컨트롤 등을 나타내는 메시지가 표시 됩니다. 그러나 자격 증명이 유효 하면 경우 Login 컨트롤 폼 인증 티켓을 만들어 및 적절 한 페이지로 사용자를 리디렉션합니다.

Login 컨트롤 네 가지 요소를 사용 하 여 적절 한 페이지를 성공적으로 로그인 시 사용자를 리디렉션하를 결정 합니다.

- Login 컨트롤에 연결 되어 있는지 로그인 페이지에 정의 된 대로 `loginUrl` 이 설정의 기본값은 있으며 폼 인증 구성에서 설정`Login.aspx`
- 존재는 `ReturnUrl` querystring 매개 변수
- Login 컨트롤의 값 [ `DestinationUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)
- `defaultUrl` 인증 구성 설정의 폼에 지정 된 값이이 설정의 기본값은 Default.aspx;

그림 4는 방법을 보여 주며 로그인 컨트롤 이러한 4 개의 매개 변수를 사용 하 여 해당 페이지를 적절 한 의사 결정에 도달 하 게 합니다.


[![페이지에 로그인 컨트롤 추가](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**그림 4**: 페이지에 로그인 컨트롤을 추가 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png))


브라우저를 통해 사이트를 방문 하 고 구성원 프레임 워크에 있는 기존 사용자로 로그인 하 여 로그인 컨트롤을 테스트 하려면 보십시오.

로그인 컨트롤의 렌더링 된 인터페이스는 매우 구성할 수 있습니다. 다양 한 모양을;에 영향을 주는 속성 게다가 Login 컨트롤으로 변환할 수 레이아웃 정밀 하 게 제어에 대 한 템플릿을 사용자 인터페이스 요소입니다. 이 단계의 나머지 부분에는 모양 및 레이아웃 사용자 지정 하는 방법을 검사 합니다.

### <a name="customizing-the-login-controls-appearance"></a>로그인 컨트롤의 모양 사용자 지정

(로그에) 제목과 함께 사용자 인터페이스를 렌더링 하는 로그인 컨트롤의 기본 속성 설정이, 확인란을 선택 하 고 로그인 단추 다음 때는 암호 저장 사용자 이름 및 암호 입력에 대 한 텍스트 상자 및 레이블을 제어 합니다. 이러한 요소 들의 모양은 모든 로그인 컨트롤의 다양 한 속성을 통해 구성할 수 있습니다. 또한,--새 사용자 계정을 만들려면 페이지에 대 한 링크와 같은 추가 사용자 인터페이스 요소는 속성 또는 두 개를 설정 하 여 추가할 수 있습니다.

우리의 로그인 컨트롤의 모양을 구성 gussy를 몇 분 정도 지출 보겠습니다. 이후는 `Login.aspx` 페이지에 이미 로그인을 표시 하는 페이지의 위쪽에 텍스트, 로그인 컨트롤의 제목은 불필요 합니다. 따라서 지울는 [ `TitleText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) 로그인 컨트롤의 제목을 제거 하려면 값입니다.

사용자 이름: 및 암호: 통해 두 개의 TextBox 컨트롤의 왼쪽에 레이블을 사용자 지정할 수는 [ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) 및 [ `PasswordLabelText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)각각. 사용자 이름 바꿔보겠습니다: Username을 읽기 위한 레이블: 합니다. 레이블 및 텍스트 스타일을 통해 구성할 수는 [ `LabelStyle` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) 및 [ `TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)각각.

암호 저장 로그인 컨트롤을 통해 다음 시간 CheckBox의 Text 속성을 설정할 수 있습니다 [ `RememberMeText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx), 기본 검사 상태를 통해 구성할 수는 [ `RememberMeSet` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx)(어떤 기본값: False)입니다. 계속 해 설정 된 `RememberMeSet` 기본적으로 속성을 다음 시간을 메일 주소 저장 확인란 있도록 true로 확인 됩니다.

Login 컨트롤은 해당 사용자 인터페이스 컨트롤의 레이아웃을 조정 하기 위한 두 가지 속성을 제공 합니다. [ `TextLayout` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) 나타냅니다 있는지 여부를 사용자 이름: 및 암호: 레이블 또는 위에 (기본값) 이면 해당 해당 입력란의 왼쪽에 나타납니다. [ `Orientation` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) 사용자 이름 및 암호 입력 세로로 배치 있는지 여부를 나타냅니다 (나란히) 또는 가로로 합니다. 이러한 두 속성을 해당 기본값으로 설정 유지 하려고 하지만 그에 따른 결과 보려면 기본이 아닌 값으로 이러한 두 속성을 설정 해 보고을 확인해 보십시오.

> [!NOTE]
> 다음 섹션에서 로그인 컨트롤의 레이아웃을 구성 살펴보도록 하겠습니다 템플릿을 사용 하 여 레이아웃 컨트롤의 사용자 인터페이스 요소의 정확한 레이아웃을 정의 합니다.


설정 하 여 로그인 컨트롤의 속성 설정을 마무리는 [ `CreateUserText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) 및 [ `CreateUserUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) 아직 등록 not? 계정을 만듭니다. 및 `~/Membership/CreatingUserAccounts.aspx`각각. 하이퍼링크에서 만든 페이지를 가리키는 로그인 컨트롤의 인터페이스를 추가 하는이 <a id="Tutorial05"> </a> [이전 자습서](creating-user-accounts-vb.md)합니다. Login 컨트롤 [ `HelpPageText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) 및 [ `HelpPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) 및 [ `PasswordRecoveryText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) 및 [ `PasswordRecoveryUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) 도움말 페이지 및 암호 복구 페이지에 대 한 링크를 렌더링 하는 동일한 방식으로 작동 합니다.

속성 변경 후 로그인 컨트롤의 선언적 태그 및 모양 비슷해야 그림 5에 표시 된 것입니다.


[![로그인 컨트롤의 속성 값의 모양을 지정합니다](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**그림 5**: The 로그인 컨트롤의 속성 값 지정 해당 모양 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png))


### <a name="configuring-the-login-controls-layout"></a>로그인 컨트롤의 레이아웃을 구성합니다.

로그인 웹 컨트롤의 기본 사용자 인터페이스를 html에서 인터페이스 레이아웃 `<table>`합니다. 그러나 렌더링 된 출력을 더욱 세밀 하 게 제어 해야 경우에 어떻게? 바꿀 것인지 우리는 `<table>` 일련의 `<div>` 태그입니다. 또는 응용 프로그램 인증에 대 한 추가 자격 증명을 필요로 하는 경우에 어떻게? 예를 들어, 많은 재무 웹 사이트 뿐만 아니라 사용자 이름 및 암호 하지만 또한 개인 식별 번호 (PIN) 또는 기타 식별 정보를 제공 하는 사용자를 필요 합니다. 어떤 이유를 수 있기 Login 컨트롤을 명시적으로 선언 인터페이스의 태그를 정의할 수 있습니다를 템플릿으로 변환 하려면.

다음 두 가지 추가 자격 증명을 수집 하도록 로그인 컨트롤을 업데이트 하기 위해 수행 해야 합니다.

1. 추가 자격 증명을 수집 하려면 웹 컨트롤을 포함 하도록 로그인 컨트롤의 인터페이스를 업데이트 합니다.
2. 사용자가 자신의 사용자 이름과 암호가 올바른지, 그리고 추가 자격 증명은 너무 유효 하는 경우에 인증 되도록 로그인 컨트롤의 내부 인증 논리를 재정의 합니다.

첫 번째 작업을 수행 하려면 하 Login 컨트롤을 템플릿으로 변환 하 고 필요한 웹 컨트롤을 추가 해야 합니다. 두 번째 작업의 경우와 로그인 컨트롤의 인증 논리 대체 될 수 있습니다는 컨트롤에 대 한 이벤트 처리기를 만들어 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)합니다.

자신의 사용자 이름, 암호 및 전자 메일 주소에 대 한 메시지를 표시 하 고 제공 된 전자 메일 주소는 파일에서 전자 메일 주소를 일치 하는 경우에 사용자를 인증에 보겠습니다 Login 컨트롤을 업데이트 합니다. 먼저 로그인 컨트롤의 인터페이스를 템플릿으로 변환 해야 합니다. 로그인 컨트롤의 스마트 태그에서 변환 서식 파일 옵션을 선택 합니다.


[![Login 컨트롤을 템플릿으로 변환](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**그림 6**: Login 컨트롤을 템플릿으로 변환 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png))


> [!NOTE]
> Login 컨트롤을 미리 template 버전으로 되돌리려면 컨트롤의 스마트 태그에서 다시 설정 링크를 클릭 합니다.


Login 컨트롤을 템플릿으로 변환 추가 `LayoutTemplate` HTML 요소와 사용자 인터페이스를 정의 하는 웹 컨트롤을 사용 하 여 컨트롤의 선언적 태그에 있습니다. 그림 7에서 볼 수 있듯이 컨트롤을 템플릿으로 변환 제거 다양 한 속성이 속성 창에서와 같은 `TitleText`, `CreateUserUrl`조각과, 이후 템플릿을 사용 하는 경우 이러한 속성 값은 무시 됩니다.


[![적은 수의 속성을 템플릿으로 사용할 수 있는 경우는 로그인 컨트롤은 변환 됩니다.](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**그림 7**: 적은 수의 속성을 템플릿으로 사용할 수 있는 경우는 로그인 컨트롤은 변환 됩니다 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png))


에 HTML 태그는 `LayoutTemplate` 필요에 따라 수정 될 수 있습니다. 마찬가지로, 자유롭게 서식 파일을 새 웹 컨트롤을 추가 합니다. 그러나 반드시 해당 로그인 컨트롤의 핵심 웹 컨트롤 템플릿을에 유지 되 고 할당 된 상태로 유지 `ID` 값입니다. 특히, 제거 하거나 마십시오 이름 바꾸기는 `UserName` 또는 `Password` 텍스트 상자는 `RememberMe` 확인란을 선택은 `LoginButton` 단추를는 `FailureText` 레이블 또는 `RequiredFieldValidator` 컨트롤입니다.

방문자의 전자 메일 주소를 수집 하려면 서식 파일에 텍스트 상자를 추가 해야 합니다. 테이블 행 간의 다음 선언적 태그를 추가 (`<tr>`)를 포함 하는 `Password` 텍스트 상자 및 메일 주소 저장 다음 보유 하는 테이블 행 시간 확인란을 선택 합니다.

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

추가한 후의 `Email` TextBox 브라우저를 통해 페이지를 방문 합니다. 그림 8 에서처럼 로그인 컨트롤의 사용자 인터페이스는 이제 세 번째 textbox를 포함 합니다.


[![Login 컨트롤 사용자의 전자 메일 주소에 대 한 Textbox를 이제 포함](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**그림 8**: Login 컨트롤 이제 사용자의 전자 메일 주소에 대 한 Textbox를 포함 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png))


Login 컨트롤이 시점에서 계속 사용 하 여 `Membership.ValidateUser` 메서드를 제공된 된 자격 증명의 유효성을 검사 합니다. 에 값을 입력 하는 도구 모음에서 `Email` 텍스트 상자에는 사용자 로그인 할 수 있는지 여부에 영향을 주지 않습니다. 3 단계는 사용자 이름 및 암호 유효 하 고 제공 된 전자 메일 주소가 파일에서 전자 메일 주소와 일치 하는 경우 자격 증명이 있는 유효한 것만 로그인 컨트롤의 인증 논리를 재정의 하는 방법을 살펴보겠습니다.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3 단계: 로그인 컨트롤의 인증 논리를 수정합니다.

그녀는 방문자가 제공 하는 경우 자격 증명 및 로그인 단추를 다시 게시 계속 클릭 및 로그인 인증 워크플로 통해 진행 될 때 제어 합니다. 발생 시켜 워크플로 시작에서 [ `LoggingIn` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)합니다. 이 이벤트와 연결 된 모든 이벤트 처리기를 설정 하 여 작업에서 로그를 취소할 수는 `e.Cancel` 속성을 `True`합니다.

워크플로 발생 시켜 진행 되는 작업에 대 한 로그를 취소 하지는 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)합니다. 경우에 대 한 이벤트 처리기는 `Authenticate` 이벤트,이 제공 된 자격 증명이 유효한 지 여부를 결정 합니다. Login 컨트롤에 사용 하 여 이벤트 처리기를 지정 하는 경우는 `Membership.ValidateUser` 메서드는 자격 증명의 유효성을 확인 합니다.

제공 된 자격 증명이 유효 원본인 경우 폼 인증 티켓 생성 되는 [ `LoggedIn` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) 이 발생 하면 사용자가 적절 한 페이지로 리디렉션되 합니다. 그러나 자격 증명이 유효 하지 여겨지는 경우 하면 [ `LoginError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) 발생 하 고 사용자에 게 자격 증명 잘못 되었음을 알리는 메시지가 표시 됩니다. 기본적으로 로그인 실패 시 컨트롤 설정 해당 `FailureText` 레이블을 지정 (로그인 하지 못했습니다 오류 메시지를 컨트롤의 Text 속성. 다시 시도 하십시오). 그러나 경우 Login 컨트롤 [ `FailureAction` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) 로 설정 된 `RedirectToLoginPage`, 로그인 제어 문제 다음는 `Response.Redirect` querystring 매개 변수를 추가 합니다. 로그인 페이지에 `loginfailure=1` (때문에 로그인 오류 메시지를 표시할 컨트롤)입니다.

그림 9에서는 인증 워크플로의 순서도 제공합니다.


[![Login 컨트롤 인증 워크플로](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**그림 9**: The 로그인 컨트롤의 인증 워크플로 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png))


> [!NOTE]
> 사용 시기에 있는지는 `FailureAction`의 `RedirectToLogin` 옵션 페이지에서 다음 시나리오를 고려 합니다. 지금 당장 우리 `Site.master` 마스터 페이지에는 현재, Hello, 군에 표시할 텍스트를 익명 사용자가 방문 하는 경우 왼쪽된 열에 있지만 해당 텍스트 로그인 컨트롤로 대체 하 려 한다고 가정 합니다. 이렇게 되 면 익명 사용자 대신 로그인 페이지를 직접 방문 하 여 사이트에서 모든 페이지에서 로그인 할 수 있습니다. 그러나 사용자는 마스터 페이지에서 렌더링 되는 로그인 컨트롤을 통해 로그인 할 수 없는 경우, 좋을 수 있습니다 로그인 페이지로 리디렉션합니다 (`Login.aspx`) 추가 지침, 링크 및 링크 만들기와 같은 다른 도움말-가능성이 해당 페이지에 포함 되어 있으므로 새 계정 또는 마스터 페이지에 추가 되지 않은 손실된 암호-검색 합니다.


### <a name="creating-theauthenticateevent-handler"></a>만들기는`Authenticate`이벤트 처리기

이 사용자 지정 인증 논리를 연결 하려면 로그인 컨트롤에 대 한 이벤트 처리기를 만들려면 해야 `Authenticate` 이벤트입니다. 에 대 한 이벤트 처리기를 만드는 `Authenticate` 이벤트는 다음 이벤트 처리기 정의 생성 합니다.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

볼 수 있듯이 `Authenticate` 형식의 개체를 전달 된 이벤트 처리기 [ `AuthenticateEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) 두 번째 입력된 매개 변수로 합니다. `AuthenticateEventArgs` 라는 부울 속성을 포함 하는 클래스 `Authenticated` 제공 된 자격 증명이 유효한 지 여부를 지정 하는 데 사용 되는 합니다. 이 작업, 제공 된 자격 증명이 유효한 지 여부를 결정 하는 코드를 작성 하 고 설정 하려면 그런 다음,이 `e.Authenticate` 속성 적절 하 게 합니다.

### <a name="determining-and-validating-the-supplied-credentials"></a>확인 하 고 제공된 된 자격 증명 유효성 검사

Login 컨트롤을 사용 하 여 [ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) 및 [ `Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) 사용자가 입력 한 사용자 이름 및 암호 자격 증명을 확인 하려면. 추가 웹 컨트롤에 입력 된 값을 확인 하기 위해 (같은 `Email` TextBox 이전 단계에서 추가 되었습니다)를 사용 하 여 `LoginControlID.FindControl`("*`controlID`*") 웹에 대 한 프로그래밍 참조를 가져올 수 서식 파일에서 컨트롤 `ID` 속성이  *`controlID`* 합니다. 예를 들어에 대 한 참조를 얻으려고는 `Email` 텍스트 상자 다음 코드를 사용 합니다.

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

사용자의 자격 증명의 유효성을 검사 하기 위해 두 개의 작업을 수행 해야 합니다.

1. 제공 된 사용자 이름 및 암호가 유효한 지 확인
2. 전자 메일 주소를 입력 한 로그인을 시도 하는 사용자에 대 한 파일에 전자 메일 주소와 일치 하는지 확인 하십시오.

에서는 사용 하기만 하면 첫 번째 확인을 수행 하는 `Membership.ValidateUser` 1 단계에서에서 설명한 것 처럼 메서드. 두 번째 검사에서 TextBox 컨트롤에 입력 될 전자 메일 주소에 비교할 수 있습니다 수 있도록 사용자의 전자 메일 주소를 확인 해야 합니다. 특정 사용자에 대 한 정보를 가져오려면는 `Membership` 클래스의 [ `GetUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)합니다.

`GetUser` 메서드는 다양 한 오버 로드 합니다. 매개 변수 전달 하지 않고 사용 하는 경우 현재 로그인된 한 사용자에 대 한 정보를 반환 합니다. 특정 사용자에 대 한 정보를 가져오려면 호출 `GetUser` 자신의 사용자 이름에 전달 합니다. 두 가지 경우 모두 `GetUser` 반환는 [ `MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), 같은 속성이 있는 `UserName`, `Email`, `IsApproved`, `IsOnline`등입니다.

다음 코드는이 두 가지 검사를 구현합니다. 다음 모두 전달 `e.Authenticate` 로 설정 된 `True`, 그렇지 않으면 할당 `False`합니다.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

이 코드 위치에서 하려고 올바른 사용자 이름, 암호 및 전자 메일 주소를 입력 하는 유효한 사용자로 로그인 합니다. 다시 시도 하지만이 이번에는 의도적으로 잘못 된 메일 주소 사용 (그림 10 참조). 마지막으로, 존재 하지 않는 사용자 이름을 사용 하 여 세 번째 보세요. 첫 번째 경우에서 해야 성공적으로 로그온 사이트로 하지만 마지막 두 가지 경우에 로그인 컨트롤의 잘못 된 자격 증명 메시지가 표시 됩니다.


[![잘못 된 전자 메일 주소를 제공할 때 Tito 로그인 할 수 없습니다.](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**그림 10**: Tito 없습니다 로그의 경우 잘못 된 전자 메일 주소 제공 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png))


> [!NOTE]
> 1 단계에서에서 어떻게 the 구성원 프레임 워크 처리 잘못 된 로그인 시도 섹션에서 설명한 대로 때는 `Membership.ValidateUser` 메서드가 호출 되 고 잘못 된 자격 증명을 전달, 잘못 된 로그인 시도 추적 하 고 특정를 초과 하는 경우에 사용자를 잠그는 지정된 된 시간 창 내에서 잘못 된 시도 횟수의 임계값입니다. 사용자 지정 인증 논리 호출 이후는 `ValidateUser` 메서드, 잘못 된 암호의 유효한 사용자 이름에 대 한 잘못 된 로그인 시도 카운터를 하나씩 늘립니다 되지만이 카운터는 사용자 이름 및 암호는 유효 경우에서 증가 하지 않지만 전자 메일 주소가 올바르지 않습니다. 그럴 경우이 동작을 가능성이 해커가 사용자 이름 및 암호를 알고 있지만 무작위 기술을 사용 하 여 사용자의 메일 주소를 확인할 필요가 없기 때문에 적합 합니다.


## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4 단계: 개선 로그인 컨트롤의 잘못 된 자격 증명 메시지

사용자가 잘못 된 자격 증명으로 로그온 하려고 하는 경우 로그인 컨트롤 로그인 시도가 성공 했음을 설명 하는 메시지를 표시 합니다. 컨트롤에서 지정한 메시지를 표시 하는 특히, 해당 [ `FailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)에 로그인 시도의 기본 값이 있는 실패 했습니다. 다시 시도하세요.

회수는 여러 가지 이유로 이유는 사용자의 자격 증명이 올바르지 않을 수 있습니다.

- 사용자 이름이 존재 하지 않을 수 있습니다.
- 사용자 이름이 존재 하지만 암호가 유효 하지 않습니다.
- 사용자 이름 및 암호는 유효 하지만 사용자가 아직 승인 되지 않은
- 사용자 이름 및 암호는 유효 하지만 사용자가 잠겨 아웃 (가능성이 가장 높은 특정된 시간 프레임 내에서 잘못 된 로그인 시도 횟수를 초과 했기 때문에)

있으며 사용자 지정 인증 논리를 사용 하는 경우 다른 이유 수 있습니다. 예를 들어 코드로 안내 드린 바 3 단계는 사용자 이름 및 암호 유효할 수 있지만 하지만 전자 메일 주소가 올바르지 않을 수 있습니다.

Login 컨트롤은 이유는 자격 증명이 유효 하면에 관계 없이 동일한 오류 메시지가 표시 됩니다. 이 처럼 피드백의 사용자 계정이 아직 승인 되지 않은 경우 또는 사용자가 잠긴 혼동 될 수 있습니다. 그러나 약간 작업으로 사용 우리에 Login 컨트롤 보다 적절 한 메시지를 표시가 있을 수 있습니다.

사용자가 로그인 컨트롤에서 발생 하는 잘못 된 자격 증명으로 로그인 하려고 할 때마다 해당 `LoginError` 이벤트입니다. 계속 진행 하 고이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

Login 컨트롤을 설정 하 여 시작 하는 위의 코드 `FailureText` 속성을 기본값 (로그인 시도가 실패 했습니다. 다시 시도 하십시오). 다음 경우 제공한 사용자 이름이 기존 사용자 계정에 매핑됩니다를 확인 합니다. 그 결과 확인, 경우 `MembershipUser` 개체의 `IsLockedOut` 및 `IsApproved` 계정이 잠겼습니다 아니면 아직 승인 되지 않은 확인 하는 속성입니다. 두 경우 모두는 `FailureText` 속성이 해당 값으로 업데이트 됩니다.

이 코드를 테스트 하려면 의도적으로 하려고가 기존 사용자로 로그인 하지만 잘못 된 암호를 사용 합니다. 10 분 시간 프레임 내에서 행에 5 번이를 수행 하 고 계정이 잠기게 됩니다. 그림 11 쇼, 후속 로그인 시도 항상 (된 경우에 올바른 암호 로) 실패 하지만 이제는 좀 더 구체적인 표시 너무 많이 잘못 된 로그인 시도 횟수가 계정을 잠 궜 습니다. 계정 잠금 해제 된 메시지를 포함 하도록 관리자에 게 문의 하십시오.


[![Tito 너무 많이 잘못 된 로그인 시도 수행 하 고 잠겼습니다.](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**그림 11**: Tito 수행 너무 많이 잘못 된 로그인 시도가 되었습니다 잠겨 있는 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png))


## <a name="summary"></a>요약

이전이 자습서에서는 가격 로그인 페이지 사용자 이름/암호 쌍의 하드 코드 된 목록에 대해 제공된 된 자격 증명 유효성을 검사 합니다. 이 자습서에서는 멤버 자격 프레임 워크에 대해 자격 증명의 유효성을 검사 하려면 페이지를 업데이트 했습니다. 1 단계에서에서 사용 하 여 살펴보았습니다는 `Membership.ValidateUser` 메서드 프로그래밍 방식으로 합니다. 2 단계에서에서 교체 우리의 수동으로 만든된 사용자 인터페이스와 코드 Login 컨트롤 사용.

Login 컨트롤 표준 로그인 사용자 인터페이스를 렌더링 하 고 자동으로 멤버 자격 framework에 대 한 사용자의 자격 증명의 유효성을 검사 합니다. 또한 유효한 자격 증명을 발생 시 Login 컨트롤 사용자가에 로그인 폼 인증을 통해. 즉, 모든 기능을 갖춘 로그인 사용자 환경이 단순히 로그인으로 끌어 페이지, 선언 추가 태그 또는 코드가 필요 하면 나타납니다. 더구나 Login 컨트롤을 자세하게 매우 렌더링 된 사용자 인터페이스 및 인증 논리를 모두에 대 한 제어를 허용 합니다.

이 시점에서 방문자가 웹 사이트를 만들 수 있는 새 사용자 계정 및 로그는 사이트에 있지만 인증된 된 사용자를 기준으로 페이지에 대 한 액세스를 제한 한다는 아직. 현재 인증 또는 익명 이며, 모든 사용자 사이트에서 페이지를 볼 수 있습니다. 사용자 간 별로 사이트의 페이지에 대 한 액세스 제어와 함께에서는 해당 기능이 사용자에 따라 다릅니다. 특정 페이지를 있을 수 있습니다. 다음 자습서 권한과 로그인된 한 사용자를 기반으로 하는 페이지에 기능을 제한 하는 방법을 살펴봅니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [잠긴 및 승인 되지 않은 사용자가 사용자 지정 메시지를 표시 합니다.](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 로그인 페이지를 만듭니다.](https://msdn.microsoft.com/library/ms178331.aspx)
- [로그인 제어 기술 문서](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Login 컨트롤을 사용 하 여](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 Michael Olivero 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

>[!div class="step-by-step"]
[이전](creating-user-accounts-vb.md)
[다음](user-based-authorization-vb.md)
