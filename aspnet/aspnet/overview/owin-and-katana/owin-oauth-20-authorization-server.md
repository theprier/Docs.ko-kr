---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 권한 부여 서버 | Microsoft Docs
author: hongyes
description: 이 자습서에서는 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법을 안내 합니다. 이 유일한 outlin 고급 자습서는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/20/2014
ms.topic: article
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: e5968f8d19191c3f44e9bd58f8e22a39d8d8faff
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876555"
---
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 권한 부여 서버
====================
여 [Hongye Sun](https://github.com/hongyes), [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법을 안내 합니다. 만을 OWIN OAuth 2.0 권한 부여 서버를 만드는 단계를 설명 하는 고급 자습서입니다. 단계별 자습서 아닙니다. [샘플 코드를 다운로드](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)합니다.
> 
> > [!NOTE]
> > 이 윤곽선 해야 하는 안전한 프로덕션 응용 프로그램을 만드는 데 사용할 수 없습니다. 이 자습서는 OAuth OWIN 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법에만 개요를 제공 하는 데 사용 됩니다.
> 
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **이 자습서에 표시** | **또한에 사용할 수** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) | [Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)합니다. 최신 업데이트가 적용 된 visual Studio 2012 작동 해야 하지만,이 자습서를 거치지 않았으며 되며 일부 선택한 메뉴 및 대화 상자 서로 다릅니다. |
> | .NET 4.5 |  |
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 게시할 수 자습서로 직접 관련 되지 않는 질문이 있으면 [GitHub에서 Katana 프로젝트](https://github.com/aspnet/AspNetKatana/)합니다. 질문 및 자체 자습서에 대 한 의견에 대 한 페이지의 맨 아래에 설명 섹션을 참조 합니다.


[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) 는 제 3 자 얻으려면 응용 프로그램에 HTTP 서비스에 대 한 제한 된 액세스를 사용 하도록 설정 합니다. 보호 된 리소스에 액세스 하는 리소스 소유자의 자격 증명을 사용 하는 대신 클라이언트는 액세스 토큰을 가져옵니다 (문자열인는 특정 범위, 수명 및 다른 액세스 특성을 나타내는). 액세스 토큰 리소스 소유자의 승인으로 제 3 자 클라이언트에 권한 부여 서버에서 발급 됩니다.

이 자습서에서는 설명 합니다.

- 4 개의 권한 부여를 지원 하기 위해 권한 부여 서버를 만드는 방법 권한 유형 및 새로 고침 토큰:
    - 인증 코드 부여
    - Implicit Grant
    - 자격 증명 부여를 리소스 소유자 암호
    - 클라이언트 자격 증명 부여
- 액세스 토큰에 의해 보호 되는 리소스 서버를 만듭니다.
- OAuth 2.0 클라이언트를 만듭니다.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>전제 조건

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) 무료 또는 [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)에 표시 된 대로, **소프트웨어 버전** 페이지의 위쪽에 있습니다.
- OWIN 익숙해야 합니다. 참조 [Katana 프로젝트 시작](https://msdn.microsoft.com/magazine/dn451439.aspx) 및 [OWIN 및 Katana 새로운](index.md)합니다.
- 익숙한 [OAuth](http://tools.ietf.org/html/rfc6749) 용어를 포함 하 여 [역할](http://tools.ietf.org/html/rfc6749#section-1.1), [프로토콜 흐름](http://tools.ietf.org/html/rfc6749#section-1.2), 및 [권한 부여 허용](http://tools.ietf.org/html/rfc6749#section-1.3)합니다. [OAuth 2.0 소개](http://tools.ietf.org/html/rfc6749#section-1) 좋은 소개를 제공 합니다.

## <a name="create-an-authorization-server"></a>권한 부여 서버 만들기

이 자습서에서는 우리는 대략 다이어그램으로 사용 하는 방법을 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 및 ASP.NET MVC 권한 부여 서버를 만들어야 합니다. :이 자습서에 포함 된 각 단계 곧 완성 된 샘플에 대 한 다운로드를 제공 하기 바랍니다. 명명 된 빈 웹 응용 프로그램을 먼저 만듭니다 *AuthorizationServer* 다음 패키지를 설치 하 고 있습니다.

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- Microsoft.Owin.Security.Google (또는 다른 소셜 로그인 Microsoft.Owin.Security.Facebook 같은 패키지)

추가 [OWIN 시작 클래스](owin-startup-class-detection.md) 라는 프로젝트 루트 폴더 아래의 *시작*합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

만들기는 *앱\_시작* 폴더입니다. 선택 된 *앱\_시작* 폴더 및 다운로드 한 버전의 추가 하려면 Shift + Alt + A를 사용 하 여는 *AuthorizationServer\App\_Start\Startup.Auth.cs* 파일.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

위의 코드를 사용 하면 응용 프로그램/외부 로그인 쿠키 및 Google 인증 자체 권한 부여 서버에서 계정을 관리 하는 데 사용 됩니다.

`UseOAuthAuthorizationServer` 확장 메서드는 권한 부여 서버를 설치 하는 것입니다. 설치 옵션은 같습니다.

- `AuthorizeEndpointPath`: 요청 경로 클라이언트 응용 프로그램 사용자가 얻기 위해 사용자 에이전트를 리디렉션하는 코드 또는 토큰 발급에 동의 합니다. 예를 들어 선행 슬래시로 시작 해야 합니다 "`/Authorize`"입니다.
- `TokenEndpointPath`: 요청 경로 클라이언트 응용 프로그램이 액세스 토큰을 가져오는 직접 통신 합니다. "/Token" 처럼 선행 슬래시가로 시작 해야 합니다. 클라이언트가 발급 된 경우에 [클라이언트\_비밀](http://tools.ietf.org/html/rfc6749#appendix-A.2),이 끝점에 제공 해야 합니다.
- `ApplicationCanDisplayErrors`:로 설정 합니다. `true` 웹 응용 프로그램에 클라이언트 유효성 검사 오류에 대 한 사용자 지정 오류 페이지를 생성 하려는 경우 `/Authorize` 끝점입니다. 예를 들어 클라이언트 응용 프로그램에 다시 브라우저 리디렉션되지 않습니다 없는 경우에만 필요 때는 `client_id` 또는 `redirect_uri` 올바르지 않습니다. `/Authorize` 끝점 "oauth 볼 수 있어야 합니다. 오류 "를"oauth 합니다. ErrorDescription"및"oauth 합니다. ErrorUri"속성은 OWIN 환경에 추가 됩니다. 

    > [!NOTE]
    > 그렇지 않으면 true 이면 권한 부여 서버가 반환 하는 기본 오류 페이지 오류 세부 정보를 사용 합니다.
- `AllowInsecureHttp`: 권한 부여 및 토큰 요청이 HTTP URI 주소에 도착 하 고 들어오는 수 있도록 허용 True를 `redirect_uri` HTTP URI 주소를 요청 매개 변수를 권한을 부여 합니다. 

    > [!WARNING]
    > 보안-이 개발을 위한만 합니다.
- `Provider`: 이벤트를 처리 하는 Authorization Server 미들웨어에서 발생 하는 응용 프로그램에서 제공 개체입니다. 응용 프로그램 인터페이스를 완전히 구현 하거나의 인스턴스를 만들 수 있습니다 `OAuthAuthorizationServerProvider` 하 고이 서버는 지원 된 OAuth 흐름에 필요한 대리자를 할당 합니다.
- `AuthorizationCodeProvider`: 클라이언트 응용 프로그램에 반환할 단일 사용 권한 부여 코드를 생성 합니다. OAuth 서버의 수에 대 한 응용 프로그램 보안 **해야** 에 대 한 인스턴스를 제공 `AuthorizationCodeProvider` 하 여 생성 된 토큰이 `OnCreate/OnCreateAsync` 이벤트를 한 번만 호출에 대 한 유효한 것으로 간주 됩니다 `OnReceive/OnReceiveAsync`합니다.
- `RefreshTokenProvider`: 필요한 경우 새 액세스 토큰을 생성 하기 위해 사용할 수 있는 새로 고침 토큰을 생성 합니다. 제공 되지 권한 부여 서버는 반환 하지 않습니다에서 새로 고침 토큰은 `/Token` 끝점입니다.

## <a name="account-management"></a>계정 관리

사용자 계정 정보를 관리 하는 어떻게 OAuth 신경 쓰지 않습니다. 있기 [ASP.NET Identity](../../../identity/index.md) 담당 하는 것입니다. 이 자습서에서는 계정 관리 코드를 단순화 하 고 방금 OWIN 쿠키 미들웨어를 사용 하 여 해당 사용자가 로그인 할 수 있는지를 확인 합니다. 다음은 대 한 간단한 샘플 코드는 `AccountController`:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri` 등록 된 리디렉션 URL 사용 하 여 클라이언트의 유효성을 검사 하는 데 사용 됩니다. `ValidateClientAuthentication` 기본 체계 헤더 및 클라이언트의 자격 증명을 가져오려면 폼 본문을 검사 합니다.

로그인 페이지는 다음과 같습니다.

![](owin-oauth-20-authorization-server/_static/image1.png)

Ietf 초안 OAuth 2 검토 [인증 코드 부여](http://tools.ietf.org/html/rfc6749#section-4.1) 이제 섹션. 

**공급자** (아래 표에서)은 [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)합니다. 형식 공급자 `OAuthAuthorizationServerProvider`, 모든 OAuth 서버 이벤트가 포함 되어 있는 합니다. 

| 인증 코드 권한 섹션에서 단계 흐름 | 샘플 다운로드에는 다음이 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A)는 클라이언트는 권한 부여 끝점에는 리소스 소유자의 사용자-에이전트를 연결 하 여 흐름을 시작 합니다. 클라이언트는 클라이언트 식별자, 요청 된 범위, 로컬 상태 및 리디렉션 URI를 권한 부여 서버는 에이전트에 보냅니다 사용자-액세스 부여 (또는 거부) 후에 다시 포함 됩니다. | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) 권한 부여 서버 (사용자-에이전트)를 통해 리소스 소유자를 인증 하 고 설정 하는 리소스 소유자 부여 여부는 클라이언트의 액세스 요청을 거부 합니다. | **&lt;사용자 액세스 권한을 부여 하는 경우&gt;**  Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) 리소스 소유자를 가정 합니다. 액세스 권한을 부여, 권한 부여 서버를 제공 하는 URI 리디렉션을 사용 하 여 클라이언트 사용자 에이전트 리디렉션합니다 이전 (요청에서 또는 클라이언트 등록 하는 동안). ... |  |
|  |  |
| (D) 클라이언트는 이전 단계에서 받은 인증 코드를 포함 하 여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 합니다. 요청을 만들 때 권한 부여 서버와 클라이언트를 인증 합니다. 클라이언트 리디렉션 URI가 확인을 위한 인증 코드를 가져오는 데 포함 되어 있습니다. | Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

에 대 한 샘플 구현을 `AuthorizationCodeProvider.CreateAsync` 및 `ReceiveAsync` 생성 및 권한 부여 코드의 유효성 검사를 제어 하는 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

위의 코드 메모리 동시 사전을 사용 하 여 코드 및 id 티켓을 저장 하 고 코드를 받은 후 id를 복원 합니다. 실제 응용 프로그램에서 영구 데이터 저장소도 대체 합니다. 권한 부여 끝점의 클라이언트에 대 한 액세스 권한을 부여 하는 리소스 소유자에 대 한 않습니다. 일반적으로 사용자가 단추를 클릭 하 고 권한 부여를 확인 하도록 허용 하기 위한 사용자 인터페이스를 필요 합니다. OAuth OWIN 미들웨어 응용 프로그램 코드를를 권한 부여 끝점을 처리할 수 있습니다. 이 샘플 응용 프로그램을 사용 하 여 호출 된 MVC 컨트롤러 `OAuthController` 를 처리 합니다. 다음은 샘플 구현이입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

`Authorize` 작업은 경우 사용자가 로그인 권한 부여 서버를 먼저 확인 합니다. 그렇지 않으면 인증 미들웨어 "Application" 쿠키를 사용 하 여 인증 하도록 호출자에 게 문제를 제기 로그인 페이지로 리디렉션합니다. (위의 강조 표시 된 코드 참조). 사용자가 로그인 하는 경우 아래와 같이 권한 부여 보기를 렌더링 합니다.

![](owin-oauth-20-authorization-server/_static/image2.png)

경우는 **Grant** 단추가 선택 되는 `Authorize` 작업에 새 "Bearer" id 및이 사용 하 여 로그인을 만들어집니다. 권한 부여 서버를 전달자 토큰을 생성 하 고 JSON 페이로드를 사용 하 여 클라이언트를 다시 보내는 트리거합니다. 

### <a name="implicit-grant"></a>Implicit Grant

Ietf 초안 OAuth 2 참조 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) 이제 섹션.

 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) 그림 4에 표시 된 흐름은 흐름을 미들웨어 따릅니다는 OWIN OAuth 매핑.  

| Implicit Grant 섹션에서 단계 흐름 | 샘플 다운로드에는 다음이 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A)는 클라이언트는 권한 부여 끝점에는 리소스 소유자의 사용자-에이전트를 연결 하 여 흐름을 시작 합니다. 클라이언트는 클라이언트 식별자, 요청 된 범위, 로컬 상태 및 리디렉션 URI를 권한 부여 서버는 에이전트에 보냅니다 사용자-액세스 부여 (또는 거부) 후에 다시 포함 됩니다. | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) 권한 부여 서버 (사용자-에이전트)를 통해 리소스 소유자를 인증 하 고 설정 하는 리소스 소유자 부여 여부는 클라이언트의 액세스 요청을 거부 합니다. | **&lt;사용자 액세스 권한을 부여 하는 경우&gt;**  Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) 리소스 소유자를 가정 합니다. 액세스 권한을 부여, 권한 부여 서버를 제공 하는 URI 리디렉션을 사용 하 여 클라이언트 사용자 에이전트 리디렉션합니다 이전 (요청에서 또는 클라이언트 등록 하는 동안). ... |  |
|  |  |
| (D) 클라이언트는 이전 단계에서 받은 인증 코드를 포함 하 여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 합니다. 요청을 만들 때 권한 부여 서버와 클라이언트를 인증 합니다. 클라이언트 리디렉션 URI가 확인을 위한 인증 코드를 가져오는 데 포함 되어 있습니다. |  |

권한 부여 끝점에서는 이미 구현 되므로 (`OAuthController.Authorize` 동작) 인증 코드 부여에 대 한 자동으로 활성화할 암시적 흐름도 합니다. 참고: `Provider.ValidateClientRedirectUri` 암시적 부여 흐름 토큰을 악의적인 클라이언트 액세스를 보내지 못하도록 보호은 리디렉션 URL과 클라이언트 ID의 유효성을 검사 하는 데 사용 됩니다 ([중간자 개입 공격](https://www.owasp.org/index.php/Man-in-the-middle_attack)).

### <a name="resource-owner-password-credentials-grant"></a>자격 증명 부여를 리소스 소유자 암호

Ietf 초안 OAuth 2 참조 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 이제 섹션.

 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 그림 5에 표시 된 흐름은 흐름을 미들웨어 따릅니다는 OWIN OAuth 매핑.  

| 리소스 소유자 암호 자격 증명 부여 섹션에서 단계 흐름 | 샘플 다운로드에는 다음이 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A) 리소스 소유자의 사용자 이름 및 암호로 클라이언트를 제공합니다. |  |
|  |  |
| (B) 클라이언트는 리소스 소유자에서 받은 자격 증명을 포함 하 여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청 합니다. 요청을 만들 때 권한 부여 서버와 클라이언트를 인증 합니다. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) 권한 부여 서버 클라이언트 인증 및 리소스 소유자 자격 증명의 유효성을 검사 하 고 유효한 경우 액세스 토큰을 발급 합니다. |  |

다음은 샘플 구현에 대 한 `Provider.GrantResourceOwnerCredentials`:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> 위의 코드 되는지에 자습서의이 섹션에 설명 하 고 보안에서 사용할 수 없습니다 또는 프로덕션 앱. 리소스 소유자 자격 증명을 확인 하지는 않습니다. 모든 자격 증명이 유효 하 고 새 id를 만드는 가정 합니다. 액세스 토큰을 생성 하 고 새로 고침 토큰을 새 id가 사용 됩니다. 보안 계정 관리 코드와 코드를 바꾸십시오.


### <a name="client-credentials-grant"></a>클라이언트 자격 증명 부여

Ietf 초안 OAuth 2 참조 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 이제 섹션.

 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 그림 6에 표시 된 흐름은 흐름을 미들웨어 따릅니다는 OWIN OAuth 매핑.  

| 클라이언트 자격 증명 부여 섹션에서 단계 흐름 | 샘플 다운로드에는 다음이 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A)는 클라이언트 권한 부여 서버를 사용 하 여 인증 및 토큰 끝점에서 액세스 토큰을 요청 합니다. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) 권한 부여 서버 클라이언트를 인증 하 고 유효한 경우 액세스 토큰을 발급 합니다. |  |

다음은 샘플 구현에 대 한 `Provider.GrantClientCredentials`:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> 위의 코드 되는지에 자습서의이 섹션에 설명 하 고 보안에서 사용할 수 없습니다 또는 프로덕션 앱. 보안 클라이언트 관리 코드와 코드를 바꾸십시오.


### <a name="refresh-token"></a>새로 고침 토큰

Ietf 초안 OAuth 2 참조 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 이제 섹션.

 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 그림 2에 표시 된 흐름은 흐름을 미들웨어 따릅니다는 OWIN OAuth 매핑.  

| 클라이언트 자격 증명 부여 섹션에서 단계 흐름 | 샘플 다운로드에는 다음이 단계를 수행합니다. |
| --- | --- |
|  |  |
| (G) 클라이언트는 권한 부여 서버를 사용 하 여 인증 하 고 새로 고침 토큰을 제시 하 여 새 액세스 토큰을 요청 합니다. 클라이언트 인증 요구 사항 및 권한 부여 서버 정책 클라이언트 형식에 기반 합니다. | Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (8) 권한 부여 서버는 클라이언트를 인증 새로 고침 토큰의 유효성을 검사 및 유효한 경우 새 액세스 토큰 (및 필요에 따라 새로운 새로 고침 토큰)을 발급 합니다. |  |

다음은 샘플 구현에 대 한 `Provider.GrantRefreshToken`: 

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>액세스 토큰에 의해 보호 된 리소스 서버 만들기

빈 웹 응용 프로그램 프로젝트를 만들고 다음 프로젝트의 패키지를 설치 합니다.

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

시작 클래스를 만들고 인증 및 Web API를 구성 합니다. 참조 *AuthorizationServer\ResourceServer\Startup.cs* 샘플 다운로드에서 합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

참조 *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* 샘플 다운로드에서 합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

참조 *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* 샘플 다운로드에서 합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors` 메서드는 모든 도메인에 대해 CORS를 사용 하면 됩니다.
- `UseOAuthBearerAuthentication` 메서드를 사용 하면 OAuth 전달자 토큰 인증 미들웨어를 수신 하 고 요청에 권한 부여 헤더에서 전달자 토큰의 유효성을 검사 합니다.
- `Config.SuppressDefaultHostAuthenticaiton` 기본 억제 앱에서 인증 된 주체 호스트, 모든 요청은 수 있으므로 익명이 호출 합니다.
- `HostAuthenticationFilter` 지정 된 인증 형식에 대 한 인증을 사용할 수 있습니다. 이 경우 전달자 인증 형식입니다.

인증 된 id를 증명 하기 위해 현재 사용자의 클레임을 출력 하려면 ApiController 만듭니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

권한 부여 서버와 리소스 서버는 동일한 컴퓨터에 없는 경우 OAuth 미들웨어 다른 컴퓨터 키를 사용 하 여 암호화 하 고 전달자 액세스 토큰을 해독 합니다. 두 프로젝트 간에 동일한 개인 키를 공유 하도록 하기 위해 추가 동일한 `machinekey` 둘 다에서 설정 *web.config* 파일입니다.

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>OAuth 2.0 클라이언트를 만듭니다.

 사용 하 여는 [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 패키지를 클라이언트 코드를 단순화 합니다.

### <a name="authorization-code-grant-client"></a>권한 부여 코드 부여 클라이언트

 이 클라이언트는 MVC 응용 프로그램입니다. 액세스 토큰을 가져오는 백 엔드에서 인증 코드 부여 흐름을 트리거합니다. 아래와 같이 단일 페이지를 포함 합니다.

![](owin-oauth-20-authorization-server/_static/image3.png)

- **Authorize** 단추는이 클라이언트에 대 한 액세스 권한을 부여 하려면 리소스 관리자에 게 알리는 권한 부여 서버에 브라우저를 리디렉션합니다.
- **새로 고침** 단추 받아볼 새 액세스 토큰 및 새로 고침 토큰을 현재 새로 고침을 사용 하 여 토큰입니다.
- **리소스 API를 보호 하는 액세스** 단추는 현재 사용자의 클레임 데이터를 가져오고 페이지에 표시 하는 리소스 서버를 호출 합니다.

다음은의 샘플 코드는 `HomeController` 클라이언트의 합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth` 기본적으로 SSL이 필요 합니다. 에 추가 해야 하므로 데모 HTTP를 사용 하는 다음 구성 파일의 설정:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> 보안-프로덕션 응용 프로그램에서 SSL 해제 하지 않습니다. 이제 로그인 자격 증명 네트워크를 통해 일반 텍스트에 전송 되 고 됩니다. 위의 코드는 로컬 샘플 디버깅 및 탐색에 대해서만 합니다.


### <a name="implicit-grant-client"></a>암시적 부여 클라이언트

이 클라이언트에 JavaScript를 사용 하 여:

1. 새 창을 열고 권한 부여 서버의 권한 부여 끝점으로 리디렉션할 합니다.
2. 액세스 토큰 가져오기 URL 조각에서 다시 리디렉션할 때.

다음 그림에서는이 프로세스를 보여 줍니다.

![](owin-oauth-20-authorization-server/_static/image4.png)

클라이언트는 두 개의 페이지가 있어야: 홈 페이지 및 콜백에 대 한 기타 하나 있습니다. 다음은 샘플 코드는 JavaScript는 *Index.cshtml* 파일:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

다음은 처리 코드에 콜백 *SignIn.cshtml* 파일:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> 외부 파일에 JavaScript를 이동 하 고 Razor 태그와 함께 포함 하는 것이 좋습니다. 이 예제를 단순하게 유지 하기 위해 결합 된 합니다.


### <a name="resource-owner-password-credentials-grant-client"></a>리소스 소유자 암호 권한 부여 클라이언트 자격 증명

콘솔 응용 프로그램을 사용 하 여이 클라이언트는 데모 했습니다. 코드는 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>클라이언트 자격 증명 부여 클라이언트

리소스 소유자 암호 자격 증명 부여와 마찬가지로, 콘솔 응용 프로그램 코드는 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
