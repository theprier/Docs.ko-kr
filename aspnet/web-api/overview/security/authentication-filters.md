---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2에서에서의 인증 필터 | Microsoft Docs
author: MikeWasson
description: 인증 필터를는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 모두 지 원하는 web API 2 및 MVC 5 하지만 약간 다릅니다...
ms.author: aspnetcontent
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 6cad52e0454d685c6e96746524fbbad21e1c274d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839819"
---
<a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서의 인증 필터
====================
[Mike Wasson](https://github.com/MikeWasson)

> 인증 필터를는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 모두 지 원하는 web API 2 및 MVC 5 있지만 필터 인터페이스에 대 한 명명 규칙에서 주로 약간 다릅니다. 이 항목에서는 Web API 인증 필터를 설명 합니다.


인증 필터 개별 컨트롤러 또는 작업에 대 한 인증 체계를 설정할 수 있습니다. 이런 방식으로 앱 다른 HTTP 리소스에 대 한 다양 한 인증 메커니즘을 지원할 수 있습니다.

이 문서에서는 코드에서 보여 드리 려 합니다 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 에서 샘플 [ http://aspnet.codeplex.com ](http://aspnet.codeplex.com)합니다. 샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다. 필터 라는 클래스에서 구현 됩니다 `IdentityBasicAuthenticationAttribute`합니다. 이 샘플에서는 코드의 모든 인증 필터를 작성 하는 방법을 설명 하는 부분적 으로만 소개 하지.

## <a name="setting-an-authentication-filter"></a>인증 필터를 설정합니다.

다른 필터와 마찬가지로 인증 필터는 적용 된 컨트롤러, 작업 별로 또는 전 세계 모든 Web API 컨트롤러를 수 있습니다.

컨트롤러에 인증 필터를 적용 하려면 필터 특성을 사용 하 여 컨트롤러 클래스를 데코 레이트 합니다. 다음 코드에서는 `[IdentityBasicAuthentication]` 모든 컨트롤러의 작업에 대 한 기본 인증을 사용 하도록 설정 하는 컨트롤러 클래스를 필터링 합니다.

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

하나의 작업에 필터를 적용할 필터를 사용 하 여 작업을 데코 레이트 합니다. 다음 코드에서는 합니다 `[IdentityBasicAuthentication]` 컨트롤러의 필터링 `Post` 메서드.

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

모든 Web API 컨트롤러에 필터를 적용할 추가 **GlobalConfiguration.Filters**합니다.

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>웹 API 인증 필터를 구현합니다.

Web API 인증 필터 구현 된 [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) 인터페이스입니다. 또한에서 상속 해야 **System.Attribute**특성으로 적용 하기 위해.

합니다 **IAuthenticationFilter** 인터페이스에 두 가지 방법이 있습니다.

- **AuthenticateAsync** 있으면 요청에 자격 증명의 유효성을 검사 하 여 요청을 인증 합니다.
- **ChallengeAsync** 필요한 경우 인증 챌린지를 HTTP 응답에 추가 합니다.

에 정의 된 인증 흐름에 해당 하는 이러한 메서드 [RFC 2612](http://tools.ietf.org/html/rfc2616) 하 고 [RFC 2617](http://tools.ietf.org/html/rfc2617):

1. 클라이언트 자격 증명 권한 부여 헤더를 보냅니다. 이 문제는 일반적으로 클라이언트가 서버에서 401 (권한 없음된) 응답을 받으면 발생 합니다. 그러나 클라이언트는 401 가져오기 후 뿐 아니라 모든 요청과 함께 자격 증명을 보낼 수 있습니다.
2. 서버 자격 증명을 허용 하지 않는 경우 401 (권한 없음된) 응답을 반환 합니다. 응답에는 하나 이상의 문제를 포함 하는 Www-authenticate 헤더가 포함 됩니다. 각 문제는 서버에서 인식 하는 인증 체계를 지정 합니다.

서버는 익명 요청에 401을 반환할 수도 있습니다. 사실, 일반적으로 이것은 인증 프로세스를 시작 하는 방법입니다.

1. 클라이언트는 익명 요청을 보냅니다.
2. 서버 401을 반환합니다.
3. 클라이언트 자격 증명을 사용 하 여 요청을 다시 보냅니다.

이 흐름 모두 포함 *인증* 하 고 *권한 부여* 단계입니다.

- 클라이언트의 id를 증명 하는 인증 합니다.
- 권한 부여는 클라이언트가 특정 리소스에 액세스할 수 있는지 여부를 결정 합니다.

Web API에서 인증 필터 처리 인증을 지원 하지만 권한 부여 되지 않습니다. 권한 부여 필터 또는 내부 컨트롤러 작업 권한 부여 해야 합니다.

Web API 2 파이프라인의 흐름은 다음과 같습니다.

1. 작업을 호출 하기 전에 Web API는 해당 작업에 대 한 인증 필터의 목록을 만듭니다. 이 동작 범위, 컨트롤러 범위 및 전역 범위를 사용 하 여 필터를 포함합니다.
2. 웹 API 호출 **AuthenticateAsync** 목록의 모든 필터에 있습니다. 각 필터는 요청에 자격 증명 유효성을 검사할 수 있습니다. 필터에서 만드는 모든 필터 성공적으로 자격 증명의 유효성을 검사 합니다는 **IPrincipal** 요청에 연결 합니다. 필터 오류가 시점에서 트리거할 수도 있습니다. 그렇다면 나머지 파이프라인 실행 되지 않습니다.
3. 요청은 파이프라인의 rest를 통해 흐름 오류가 없는 것으로 가정 합니다.
4. 마지막으로 Web API 호출 마다 인증 필터 **ChallengeAsync** 메서드. 필요한 경우 응답에 챌린지를 추가 하려면이 메서드를 사용 하는 필터입니다. 일반적으로 (항상 그렇지는 않지만)는 에서처럼 발생 401 오류에 대 한 응답입니다.

다음 다이어그램은 두 가지 가능한 경우를 보여 줍니다. 첫 번째에서 인증 필터는 요청을 성공적으로 인증, 권한 부여 필터는 요청에 권한을 부여 하 고 컨트롤러 작업 200 (정상)를 반환 합니다.

![](authentication-filters/_static/image1.png)

두 번째 예제에서는 요청을 인증 하는 인증 필터는 있지만 권한 부여 필터를 401 (권한 없음)를 반환 합니다. 이 경우 컨트롤러 작업이 호출 되지 않습니다. 인증 필터를 응답에 Www-authenticate 헤더를 추가 합니다.

![](authentication-filters/_static/image2.png)

다른 조합은 가능&mdash;예를 들어, 익명 요청을 허용 하는 컨트롤러 작업을 할 경우 인증 필터를 있지만 권한이 부여 되지 않습니다.

## <a name="implementing-the-authenticateasync-method"></a>AuthenticateAsync 메서드 구현

합니다 **AuthenticateAsync** 메서드 요청을 인증 하려고 시도 합니다. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

합니다 **AuthenticateAsync** 메서드 중 하나를 수행 해야 합니다.

1. Nothing (작동 하지 않습니다).
2. 만들기는 **IPrincipal** 요청에 설정 합니다.
3. 오류 결과 설정 합니다.

요청 필터를 이해 하는 모든 자격 증명이 (1)은 옵션입니다. 옵션 (2) 이면 필터에서 요청을 성공적으로 인증 합니다. 요청 옵션 (3) 의미 오류 응답을 트리거하는 잘못 된 자격 증명 (예: 잘못 된 암호)를 했습니다.

구현에 대 한 일반적인 개요는 다음과 같습니다 **AuthenticateAsync**합니다.

1. 요청에 자격 증명을 찾습니다.
2. 자격 증명이 없는 경우 아무 작업도 수행 하 고 (아무)를 반환 합니다.
3. 자격 증명이 필터 인증 체계를 인식 하지 않습니다 하지만 아무 작업도 수행 하 고 (아무)를 반환 합니다. 파이프라인에서 다른 필터 체계를 이해 될 수 있습니다.
4. 필터를 이해 하는 자격 증명의 경우 인증 하려고 합니다.
5. 자격 증명에 잘못 된 경우 설정 하 여 401 반환 `context.ErrorResult`합니다.
6. 자격 증명에 유효한 경우 만들기는 **IPrincipal** 설정 `context.Principal`합니다.

다음 코드와 **AuthenticateAsync** 메서드에서 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플입니다. 주석은 각 단계를 나타냅니다. 코드는 여러 유형의 오류를 보여 줍니다: 없는 자격 증명, 잘못 된 자격 증명 및 잘못 된 사용자 이름/암호를 사용 하 여는 권한 부여 헤더입니다.

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>오류 결과 설정합니다.

자격 증명이 잘못 된 경우에 필터를 설정 해야 합니다 `context.ErrorResult` 에 **IHttpActionResult** 오류 응답을 야기 하는 합니다. 에 대 한 자세한 내용은 **IHttpActionResult**를 참조 하십시오 [Web API 2에서 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.

기본 인증 샘플는 `AuthenticationFailureResult` 이 용도에 적합 한 클래스입니다.

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>ChallengeAsync 구현

용도 **ChallengeAsync** 방법은 필요한 경우 인증 챌린지에 응답에 추가 하는 것입니다. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

메서드는 요청 파이프라인의 모든 인증 필터에서 호출 됩니다.

알아야 하는 것 **ChallengeAsync** 라고 *하기 전에* 만들어지고 컨트롤러 작업 실행 되기 전에 HTTP 응답 됩니다. 때 **ChallengeAsync** 가 호출 `context.Result` 포함을 **IHttpActionResult**, HTTP 응답을 만들려면 나중에 사용 되는 합니다. 있으므로 **ChallengeAsync** 는 호출을 알 수 없는 HTTP 응답에 대 한 아무 것도 아직 있습니다. 합니다 **ChallengeAsync** 메서드는 원래 값으로 대체 해야 `context.Result` 새 **IHttpActionResult**합니다. 이렇게 **IHttpActionResult** 원래 래핑해야 `context.Result`합니다.

![](authentication-filters/_static/image3.png)

원래 라고 하겠습니다 **IHttpActionResult** 는 *내부 결과*, 및 새로운 **IHttpActionResult** 합니다 *외부 결과*합니다. 외부 결과 다음을 수행 해야 합니다.

1. HTTP 응답을 만드는 내부 결과 호출 합니다.
2. 응답을 검사 합니다.
3. 필요한 경우 인증 챌린지를 응답에 추가 합니다.

다음 예제에서는 기본 인증 샘플에서 가져온 것입니다. 정의 **IHttpActionResult** 외부 결과 대 한 합니다.

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

합니다 `InnerResult` 속성 내부에 저장 **IHttpActionResult**합니다. `Challenge` 속성 Www 인증 헤더를 나타냅니다. 있음을 **ExecuteAsync** 는 먼저 호출 `InnerResult.ExecuteAsync` HTTP 응답을 만들려면 다음 필요한 경우 문제를 추가 합니다.

챌린지를 추가 하기 전에 응답 코드를 확인 합니다. 대부분의 인증 체계에만 챌린지를 추가할 경우 다음과 같이 응답은 401입니다. 그러나 일부 인증 체계 수행 성공 응답에 챌린지를 추가 합니다. 예를 들어, 참조 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).

지정 된 `AddChallengeOnUnauthorizedResult` 클래스의 실제 코드 **ChallengeAsync** 간단 합니다. 에 연결을 하면 결과 만들고 `context.Result`합니다.

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

참고: 기본 인증 예제는 확장 메서드를 배치 하 여 약간이 논리를 추상화 합니다.

## <a name="combining-authentication-filters-with-host-level-authentication"></a>호스트 수준 인증을 사용 하 여 인증 필터를 결합합니다.

"호스트 수준 인증"는 요청에 도달 하면 Web API 프레임 워크를 하기 전에 (예: IIS) 호스트에서 수행 하는 인증입니다.

대개 다음 응용 프로그램의 나머지 부분에 대 한 호스트 수준 인증을 사용 하도록 설정 하면 Web API 컨트롤러에 대 한 사용 하지 않도록 설정 하는 것이 좋습니다. 예를 들어, 호스트 수준에서 폼 인증을 사용 하도록 설정 하지만 웹 API에 대 한 토큰 기반 인증을 사용 하는 일반적인 시나리오가입니다.

Web API 파이프라인 내에서 호스트 수준 인증을 사용 하지 않으려면 호출 `config.SuppressHostPrincipal()` 구성에서 합니다. 이렇게 하면 Web API를 제거 하는 **IPrincipal** Web API 파이프라인을 입력 하는 모든 요청에서. 이 사실상 &quot;취소-인증&quot; 요청 합니다.

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 API 보안 필터가](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)
