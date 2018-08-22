---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 개별 계정 및 ASP.NET Web API 2.2에서에서 로컬 로그인을 사용 하 여 Web API 보안 유지 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 OAuth2를 사용 하 여 멤버 자격 데이터베이스에 대해 인증 하는 웹 API를 보호 하는 방법을 보여 줍니다. 자습서는 Visual Studio 201에 사용 되는 소프트웨어 버전 중...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 01d117260ef458453bee79285a37a8977221998c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827111"
---
<a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>개별 계정 및 ASP.NET Web API 2.2에서에서 로컬 로그인을 사용 하 여 Web API 보안 유지
====================
[Mike Wasson](https://github.com/MikeWasson)

[샘플 앱 다운로드](https://github.com/MikeWasson/LocalAccountsApp)

> 이 항목에서는 OAuth2를 사용 하 여 멤버 자격 데이터베이스에 대해 인증 하는 웹 API를 보호 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013 업데이트 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Web API 2.2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Id 2.1](../../../identity/index.md)


Visual Studio 2013에서 Web API 프로젝트 템플릿을 사용 하면 인증에 대 한 세 가지 옵션:

- **개별 계정입니다.** 멤버 자격 데이터베이스를 사용 하는 앱입니다.
- **조직 계정입니다.** 사용자가 Azure Active Directory, Office 365 또는 온-프레미스 Active Directory 자격 증명으로 로그인 합니다.
- **Windows 인증입니다.** 이 옵션은 인트라넷 응용 프로그램의 경우 이며 Windows Authentication IIS 모듈을 사용 합니다.

이러한 옵션에 대 한 자세한 내용은 참조 하세요. [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)합니다.

개별 계정에 로그인 할 두 가지 방법으로 제공 합니다.

- **로컬 로그인**합니다. 사용자 이름과 암호를 입력 합니다. 사이트에 등록 합니다. 응용 프로그램 멤버 자격 데이터베스에서 암호 해시를 저장합니다. 사용자가 로그인 할 때 ASP.NET Id 시스템에 암호를 확인 합니다.
- **소셜 로그인**합니다. 사용자는 Facebook, Microsoft, Google 등 외부 서비스에 로그인합니다. 여전히 앱 사용자에 대 한 항목이 멤버 자격 데이터베이스를 만들지만 모든 자격 증명을 저장 하지 않습니다. 사용자는 외부 서비스에 로그인 하 여 인증 합니다.

이 문서에서는 로컬 로그인 시나리오를 살펴봅니다. 로컬 및 소셜 로그인에 대 한 Web API는 요청을 인증 OAuth2를 사용 합니다. 그러나 자격 증명 흐름은 로컬 및 소셜 로그인에 대 한 다양 한 합니다.

이 문서에서는 사용자가 로그인 하 고 웹 API에 인증 된 AJAX 호출을 보낼 수 있는 간단한 앱을 살펴보겠습니다. 샘플 코드를 다운로드할 수 있습니다 [여기](https://github.com/MikeWasson/LocalAccountsApp)합니다. 추가 정보에는 Visual Studio에서 처음부터 샘플을 만드는 방법을 설명 합니다.

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

샘플 앱은 데이터 바인딩 및 jQuery AJAX 요청을 보내는 Knockout.js를 사용 합니다. 이 문서에 대 한 Knockout.js를 알 필요가 없습니다 있습니까 AJAX 호출에 집중 하겠습니다.

이 과정을 설명 합니다.

- 클라이언트 쪽에서 어떤 앱에서 수행 합니다.
- 서버에서 일어나 메시지가 나타납니다.
- 중간에 HTTP 트래픽을 합니다.

먼저 몇 가지 OAuth2 용어를 정의 해야 합니다.

- *리소스*합니다. 보호할 수 있는 데이터의 일부입니다.
- *리소스 서버*합니다. 리소스를 호스팅하는 서버입니다.
- *리소스 소유자*합니다. 리소스에 액세스 권한을 부여할 수 있는 엔터티. (일반적으로 사용자입니다.)
- *클라이언트*: 리소스에 액세스 하려고 하는 앱입니다. 이 문서에서는 클라이언트는 웹 브라우저입니다.
- *액세스 토큰*합니다. 리소스에 대 한 액세스 권한을 부여 하는 토큰입니다.
- *전달자 토큰*합니다. 토큰을 사용할 수 있습니다 누구나 속성을 사용 하 여 액세스 토큰에 특정 형식입니다. 즉, 클라이언트는 암호화 키 또는 전달자 토큰 사용 하 여 다른 암호 필요 하지 않습니다. 이런 이유로 전달자 토큰을 https만 사용 해야 하 고 비교적 짧은 만료 시간을 있어야 합니다.
- *권한 부여 서버*합니다. 액세스 토큰을 제공 하는 서버입니다.

응용 프로그램 권한 부여 서버와 리소스 서버 모두로 작동할 수 있습니다. Web API 프로젝트 템플릿은이 패턴을 따릅니다.

## <a name="local-login-credential-flow"></a>로컬 로그인 자격 증명 흐름

로컬 로그인에 대 한 웹 API에 사용 합니다 [리소스 소유자 암호 흐름](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) OAuth2에 정의 합니다.

1. 사용자가 클라이언트에 이름 및 암호를 입력 합니다.
2. 클라이언트가 권한 부여 서버에 이러한 자격 증명을 보냅니다.
3. 권한 부여 서버는 자격 증명을 인증 하 고 액세스 토큰을 반환 합니다.
4. 보호 된 리소스에 액세스 하려면 클라이언트는 HTTP 요청의 인증 헤더에 액세스 토큰을 포함 합니다.

![](individual-accounts-in-web-api/_static/image3.png)

선택 하면 **개별 계정** Web API 프로젝트 템플릿에서 프로젝트에 사용자 자격 증명의 유효성을 검사 하 고 토큰을 발급 하는 권한 부여 서버를 포함 합니다. 다음 다이어그램에서는 Web API 구성 요소를 기준으로 동일한 자격 증명 흐름을 보여 줍니다.

![](individual-accounts-in-web-api/_static/image4.png)

이 시나리오에서는 Web API 컨트롤러 리소스 서버로 작동 합니다. 인증 필터를 액세스 토큰의 유효성을 검사 하며 **[Authorize]** 특성 리소스를 보호 하는 데 사용 됩니다. 컨트롤러 또는 작업에 하는 경우는 **[Authorize]** 특성을 컨트롤러에 대 한 모든 요청 또는 작업을 인증 해야 합니다. 이 고, 그렇지 권한 부여가 거부 하 고 Web API를 401 (권한 없음된) 오류를 반환 합니다.

권한 부여 서버와 둘 다 호출 인증 필터를 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) OAuth2의 세부 정보를 처리 하는 구성 요소입니다. 이 자습서의 뒷부분에서 자세히의 설계를 설명 합니다.

## <a name="sending-an-unauthorized-request"></a>권한이 없는 요청을 전송

시작 하려면 앱을 실행 하 고 클릭 합니다 **API 호출** 단추입니다. 요청이 완료 되 면 오류 메시지가 나타납니다 합니다 **결과** 상자입니다. 이것은 요청에는 액세스 토큰을 포함 하지 않으므로 요청이 인증 되지 않습니다.

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

합니다 **API 호출** 단추 AJAX 요청을 보냅니다 ~/api/값이 Web API 컨트롤러 작업을 호출 합니다. AJAX 요청을 보내는 JavaScript 코드의 섹션을 다음과 같습니다. 샘플 앱에서 JavaScript 앱 코드를 모두에 Scripts\app.js 파일이 있습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

사용자가 로그인 될 때까지 전달자 토큰이 없습니다 및 따라서 없는 권한 부여 요청의 헤더에에서 있습니다. 그러면 401 오류를 반환 하는 요청 합니다.

다음은 HTTP 요청이입니다. (사용한 [Fiddler](http://www.telerik.com/fiddler) HTTP 트래픽을 캡처할 수 있습니다.)

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

전달자를 설정 하는 문제를 사용 하 여 응답 Www-authenticate 헤더에 알 수 있습니다. 서버 전달자 토큰에서 예상 하는 것이 나타내는입니다.

## <a name="register-a-user"></a>사용자 등록

에 **등록** 섹션 앱의 전자 메일 및 암호를 입력 하 고 클릭 합니다 **등록** 단추입니다.

이 샘플에 대 한 유효한 전자 메일 주소를 사용할 필요는 없지만 실제 앱 주소를 확인 합니다. (참조 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) 암호를 사용 하 여 "Password1!"와 같이 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 사용 하 여 합니다. 클라이언트 쪽 유효성 검사 아웃 두었습니다 간단히 유지 하기 위해 앱 암호 형식에 문제가 있으면 400 (잘못 된 요청) 오류가 발생을 얻을 수 있습니다.

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

합니다 **등록** 단추 ~/api/Account/Register에 POST 요청이 전송 /입니다. 요청 본문에는 이름 및 암호를 보유 하는 JSON 개체입니다. 요청을 보내는 JavaScript 코드는 다음과 같습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

이 요청을 처리 합니다 `AccountController` 클래스입니다. 내부적으로 `AccountController` ASP.NET Id를 사용 하 여 멤버 자격 데이터베이스를 관리 합니다.

Visual Studio에서 앱을 로컬로 실행 하는 경우 사용자 계정은 AspNetUsers 테이블에서 LocalDB에 저장 됩니다. Visual Studio에서 테이블을 보려면 클릭 합니다 **보기** 메뉴에서 **서버 탐색기**를 차례로 확장 **데이터 연결**.

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>액세스 토큰 가져오기

지금까지 우리가 수행 하지 않은 모든 OAuth 있지만 이제 살펴보겠습니다 OAuth 권한 부여 서버 작업에 대 한 액세스 토큰을 요청할 때. 에 **로그인** 메일과 암호를 입력 하 고 클릭 하는 샘플 앱의 영역 **로그인**합니다.

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

합니다 **로그인** 단추 토큰 끝점에 요청을 보냅니다. 다음 양식 url로 인코딩된 데이터를 포함 하는 요청 본문:

- grant\_type: "password"
- 사용자 이름: &lt;사용자의 전자 메일&gt;
- 암호: &lt;암호&gt;

AJAX 요청을 보내는 JavaScript 코드는 다음과 같습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

요청이 성공 하는 경우 권한 부여 서버는 응답 본문에 액세스 토큰을 반환 합니다. 토큰 API에 요청을 보낼 때 나중에 사용할 세션 저장소에 저장 된 알 수 있습니다. 일부 형태의 인증 (예: 쿠키 기반 인증)와 달리 브라우저 포함 되지 않습니다 자동으로 액세스 토큰은 후속 요청에서. 응용 프로그램이 있으므로 명시적으로 수행 해야 합니다. 좋은 것을 제한 하므로 [CSRF 취약점으로 인 한](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

요청에 사용자의 자격 증명을 확인할 수 있습니다. 있습니다 *해야* HTTPS를 사용 하 여 전송 계층 보안을 제공 합니다.

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

가독성을 위해 JSON을 들여쓰기 있습니까 고 매우 긴 액세스 토큰을 잘립니다.

합니다 `access_token`, `token_type`, 및 `expires_in` 속성은 OAuth2 사양에서 정의 됩니다. 다른 속성 (`userName`, `.issued`, 및 `.expires`)는 정보 제공을 위해서만 합니다. 이러한 추가 속성을 추가 하는 코드를 찾을 수 있습니다는 `TokenEndpoint` 메서드를 /Providers/ApplicationOAuthProvider.cs 파일입니다.

## <a name="send-an-authenticated-request"></a>인증 된 요청을 보내기

전달자 토큰을 만들었으므로 API에 인증 된 요청을 가능 했습니다. 이 요청에 Authorization 헤더를 설정 하 여 이루어집니다. 클릭 합니다 **API 호출** 하려면 단추를 다시 참조 하세요.

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>로그 아웃

브라우저는 자격 증명이 나 액세스 토큰을 캐시 하지 않습니다, 때문에 로그 아웃 토큰을 세션 저장소에서 제거 하 여 "무시"의 하기만 하면 됩니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>개별 계정을 프로젝트 템플릿 이해

선택 하면 **개별 계정** 프로젝트는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿에 포함 되어 있습니다.

- OAuth2 권한 부여 서버입니다.
- 사용자 계정 관리에 대 한 Web API 끝점
- 사용자 계정을 저장 하는 것에 대 한 EF 모델입니다.

이러한 기능을 구현 하는 기본 응용 프로그램 클래스는 다음과 같습니다.

- `AccountController`. 사용자 계정을 관리 하기 위한 Web API 끝점을 제공 합니다. `Register` 작업은이 자습서에서 사용 하는 유일한 알고리즘입니다. 클래스의 다른 메서드는 암호 재설정, 소셜 로그인 및 기타 기능을 지원합니다.
- `ApplicationUser`/Models/IdentityModels.cs에 정의 합니다. 이 클래스는 멤버 자격 데이터베이스에서 사용자 계정에 대 한 EF 모델입니다.
- `ApplicationUserManager`/App에 정의 된\_이 클래스에서 파생 됩니다 Start/IdentityConfig.cs [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) 암호 등을 확인 하는 새 사용자 만들기와 같은 사용자 계정에서 작업을 수행 하 고 자동으로 유지 데이터베이스를 변경 합니다.
- `ApplicationOAuthProvider`. 이 개체는 OWIN 미들웨어를 크롤링합니다 및 미들웨어에서 발생 하는 이벤트를 처리 합니다. 파생 되므로 [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)합니다.

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>권한 부여 서버를 구성합니다.

StartupAuth.cs, 다음 코드는 OAuth2 권한 부여 서버를 구성합니다.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` 속성에는 권한 부여 서버 끝점 URL 경로입니다. URL는 전달자 토큰을 가져오기 위해 해당 앱을 사용 합니다.

`Provider` 속성은 OWIN 미들웨어에 연결 하 고 미들웨어에서 발생 하는 이벤트를 처리 하는 공급자를 지정 합니다.

앱 토큰을 가져오려면 하려고 할 때의 기본 흐름을 다음과 같습니다.

1. 앱의 요청을 보내 액세스 토큰을 가져오려면 ~ n /입니다.
2. OAuth 미들웨어 호출 `GrantResourceOwnerCredentials` 공급자입니다.
3. 공급자 호출을 `ApplicationUserManager` 클레임 id를 만들고 자격 증명의 유효성을 검사 합니다.
4. 작업에 성공 하면 공급자는 토큰을 생성 하는 데 사용 되는 인증 티켓을 만듭니다.

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth 미들웨어는 사용자 계정에 대 한 아무것도 알지 못합니다. 공급자는 미들웨어 및 ASP.NET Id 간에 통신합니다. 권한 부여 서버를 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [OWIN OAuth 2.0 권한 부여 서버](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)합니다.

### <a name="configuring-web-api-to-use-bearer-tokens"></a>전달자 토큰을 사용 하도록 Web API 구성

에 `WebApiConfig.Register` 메서드를 다음 코드에서는 Web API 파이프라인에 대 한 인증을 설정 합니다.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

합니다 **HostAuthenticationFilter** 클래스를 사용 하면 전달자 토큰을 사용 하 여 인증 합니다.

합니다 **SuppressDefaultHostAuthentication** 메서드 Web API 요청에는 IIS 또는 OWIN 미들웨어에서 Web API 파이프라인에 도달 하기 전에 발생 하는 인증을 무시 하도록 지시 합니다. 이런 방식으로 웹 API만 전달자 토큰을 사용 하 여 인증을 제한할 수 있습니다.

> [!NOTE]
> 특히, 앱의 MVC 부분이 폼 인증 쿠키에 자격 증명을 저장 하는 사용할 수 있습니다. 쿠키 기반 인증 CSRF 공격을 방지 하기 위해 위조 방지 토큰을 사용을 해야 합니다. 웹 Api에 대 한 문제가 위조 방지 토큰을 클라이언트로 보낼 웹 API에 대 한 편리한 방법이 없기 때문입니다. (이 문제에 자세한 배경 정보를 참조 하세요 [Web API에서 CSRF 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md).) 호출 **SuppressDefaultHostAuthentication** Web API를 쿠키에 저장 된 자격 증명에서 CSRF 공격에 취약 하지 않도록 합니다.


클라이언트가 보호 된 리소스를 요청 하면 Web API 파이프라인에서 어떻게 다음과 같습니다.

1. 합니다 **HostAuthentication** 토큰 유효성 검사에 OAuth 미들웨어를 호출 하는 필터입니다.
2. 미들웨어는 토큰 클레임 id를 변환합니다.
3. 이 시점에서 요청은 *인증* 있지만 *권한이*합니다.
4. 클레임 id를 검사 하는 권한 부여 필터입니다. 클레임에는 해당 리소스에 대 한 사용자의 권한 부여를 요청 권한을 부여 합니다. 기본적으로 **[Authorize]** 특성은 인증 된 모든 요청을 인증 합니다. 그러나 다른 클레임 하거나 역할에서 권한을 부여할 수 있습니다. 자세한 내용은 [인증 및 권한 부여 Web API에서](authentication-and-authorization-in-aspnet-web-api.md)합니다.
5. 이전 단계에 성공한 경우 컨트롤러는 보호 된 리소스를 반환 합니다. 그렇지 않으면 클라이언트를 401 (권한 없음된) 오류가 나타납니다.

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Id](../../../identity/index.md)
- [VS2013 RC에 대 한 SPA 템플릿의 보안 기능을 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)합니다. Sun Hongye에서 MSDN 블로그 게시물.
- [템플릿-파트 2 계정 웹 API 개별 분석: 로컬 계정](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)합니다. Dominick Baier 블로그 게시물입니다.
- [인증 및 OWIN 사용 하 여 웹 API를 호스팅할](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)합니다. 적절 한 설명은 `SuppressDefaultHostAuthentication` 및 `HostAuthenticationFilter` Brock Allen 여 합니다.
- [VS 2013 템플릿에서 ASP.NET Id에서 프로필 정보를 사용자 지정](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)합니다. Pranav rastogi MSDN 블로그 게시물입니다.
- [UserManager 클래스 ASP.NET Id에 대 한 요청 수명 관리 당](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)합니다. Suhas Joshi의 좋은 설명 MSDN 블로그 게시물을 `UserManager` 클래스입니다.
