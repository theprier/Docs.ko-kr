---
uid: web-api/overview/security/authentication-filters
title: "ASP.NET Web API 2의에서 인증 필터 | Microsoft Docs"
author: MikeWasson
description: "인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 둘 다 지원 web API 2 및 MVC 5 하지만 약간 다른..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/25/2014
ms.topic: article
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 7c704cc351876b49ec143a49b25cc0ca83876e06
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2의에서 인증 필터
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 둘 다 지원 web API 2 및 MVC 5 있지만 필터 인터페이스에 대 한 명명 규칙에서 주로 약간 다릅니다. 이 항목에서는 웹 API 인증 필터를 설명 합니다.


인증 필터 개별 컨트롤러 또는 동작에 대 한 인증 체계를 설정할 수 있습니다. 이런 방식으로 앱 다른 HTTP 리소스에 대 한 다른 인증 메커니즘을 지원할 수 있습니다.

이 문서에서는 코드에서 보여 드리 려 고 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플 [http://aspnet.codeplex.com](http://aspnet.codeplex.com)합니다. 이 샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다. 필터 라는 클래스에서 구현 되 `IdentityBasicAuthenticationAttribute`합니다. 모든 샘플의 코드는 인증 필터를 작성 하는 방법을 보여 주는 해당 부분만 소개 하지 합니다.

## <a name="setting-an-authentication-filter"></a>인증 필터를 설정합니다.

다른 필터와 마찬가지로 인증 필터 적용 된 컨트롤러, 작업 별로 또는 전체적으로 모든 Web API 컨트롤러 수 있습니다.

컨트롤러에는 인증 필터를 적용 하려면 필터 특성으로 컨트롤러 클래스 데코 레이트 합니다. 다음 코드에서는 `[IdentityBasicAuthentication]` 모든 컨트롤러의 작업에 대 한 기본 인증을 사용할 수 있는 컨트롤러 클래스에 대 한 필터입니다.

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

한 동작으로 필터를 적용 하려면 작업 필터와 데코 레이트 합니다. 다음 코드에서는 `[IdentityBasicAuthentication]` 컨트롤러의에 대 한 필터 `Post` 메서드.

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

모든 Web API 컨트롤러에 필터를 적용 하려면에 추가 **GlobalConfiguration.Filters**합니다.

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>웹 API 인증 필터를 구현합니다.

인증 필터 Web API에서 구현 된 [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) 인터페이스입니다. 상속 해야 **System.Attribute**을 특성으로 적용 하도록 합니다.

**IAuthenticationFilter** 인터페이스에는 두 가지 방법:

- **AuthenticateAsync** 있는 경우 요청에 자격 증명을 확인 하 여 요청을 인증 합니다.
- **ChallengeAsync** 필요한 경우 HTTP 응답에 대 한 인증 챌린지를 추가 합니다.

에 정의 된 인증 흐름에 해당 하는 이러한 메서드 [RFC 2612](http://tools.ietf.org/html/rfc2616) 및 [RFC 2617](http://tools.ietf.org/html/rfc2617):

1. 클라이언트 자격 증명을 인증 헤더에 보냅니다. 이 문제는 일반적으로 클라이언트에서 서버에서 401 (권한 없음된) 응답을 받은 후에 발생 합니다. 그러나 클라이언트는 401 가져오기 후 뿐 아니라 모든 요청에 자격 증명을 보낼 수 있습니다.
2. 서버 자격 증명을 허용 하지는 401 (권한 없음된) 응답을 반환 합니다. 응답에는 하나 이상의 문제를 포함 하는 Www-authenticate 헤더가 포함 되어 있습니다. 각 시도 서버에서 인식 하는 인증 체계를 지정 합니다.

서버는 익명 요청에서 401을 반환할 수도 있습니다. 사실, 일반적으로 이것은 인증 프로세스가 시작 되는 방식:

1. 클라이언트는 익명 요청을 보냅니다.
2. 서버 401을 반환합니다.
3. 클라이언트 자격 증명을 사용 하 여 요청을 다시 보냅니다.

이 흐름을에 둘 다 *인증* 및 *권한 부여* 단계입니다.

- 인증은 클라이언트의 id를 증명합니다.
- 권한 부여 클라이언트 특정 리소스에 액세스할 수 있는지 여부를 결정 합니다.

웹 API에 인증 필터 권한 부여 하지 않지만 인증을 처리합니다. 컨트롤러 작업 내부에서 실행 되거나 권한 부여 필터에 의해 권한 부여를 수행 해야 합니다.

Web API 2 파이프라인에서 흐름은 다음과 같습니다.

1. 동작을 호출 하기 전에 웹 API에는 해당 작업에 대 한 인증 필터의 목록을 만듭니다. 동작 범위, 범위 컨트롤러 및 글로벌 범위를 사용 하 여 필터를 포함 합니다.
2. 웹 API 호출 **AuthenticateAsync** 목록에는 모든 필터에 있습니다. 각 필터에는 요청에 자격 증명 유효성을 검사할 수 있습니다. 모든 필터에 성공적으로 자격 증명 유효성을 검사 하는 경우 필터 만듭니다는 **IPrincipal** 요청에 연결 합니다. 또한 필터 오류가이 시점에서 트리거할 수 있습니다. 이 경우 나머지 파이프라인 실행 되지 않습니다.
3. 요청은 오류가 없는 경우 파이프라인의 나머지 부분을 이동 합니다.
4. Web API에서 모든 인증 필터를 호출 하는 마지막으로, **ChallengeAsync** 메서드. 필요한 경우를 응답에 챌린지를 추가 하려면이 메서드를 사용 하는 필터. 일반적으로 (항상 그렇지는 않지만)는에서 사용 하는 발생할 401 오류에 응답 합니다.

다음 다이어그램은 두 가지 가능한 경우를 보여 줍니다. 첫 번째 호출 인증 필터를 성공적으로 요청 인증, 권한 부여 필터는 요청에 권한을 부여 하 고 컨트롤러 작업 200 (정상)를 반환 합니다.

![](authentication-filters/_static/image1.png)

두 번째 예제에서는 인증 필터는 요청을 인증 하지만 권한 부여 필터 401 (권한 없음)을 반환 합니다. 이 경우에 컨트롤러 동작 호출 되지 않습니다. 인증 필터를 응답에 Www 인증 헤더를 추가합니다.

![](authentication-filters/_static/image2.png)

다른 조합은 가능한&mdash;예를 들어 컨트롤러 동작 익명 요청을 허용 하는 경우 할 수 있습니다는 인증 필터 하지만 없습니다.

## <a name="implementing-the-authenticateasync-method"></a>AuthenticateAsync 메서드 구현

**AuthenticateAsync** 메서드는 요청을 인증 하려고 합니다. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**AuthenticateAsync** 메서드는 다음 중 하나를 수행 해야 합니다.

1. Nothing (아무)입니다.
2. 만들기는 **IPrincipal** 요청에 설정 합니다.
3. 오류 결과 설정 합니다.

요청 옵션 (1) 의미 필터 이해할 수 있는 자격 증명을 변수가 없습니다. 옵션 (2) 의미 필터에서 요청을 성공적으로 인증 합니다. 요청 옵션 (3) 이면 오류 응답을 트리거하는 잘못 된 자격 증명 (예: 잘못 된 암호)로, 했습니다.

다음은 구현에 대 한 일반 개요 **AuthenticateAsync**합니다.

1. 요청에 자격 증명을 찾습니다.
2. 자격 증명이 없는 경우 아무 작업도 수행 하 고 (op)를 반환 합니다.
3. 자격 증명 하는 경우 필터는 인증 체계를 인식 하지 않으므로 아무 작업도 수행 하 고 (op)를 반환 합니다. 파이프라인에서 다른 필터는 구성표를 이해할 수도 있습니다.
4. 필터를 이해 하는 자격 증명 경우 인증 하려고 합니다.
5. 잘못 된 자격 증명을 설정 하 여 401 반환 `context.ErrorResult`합니다.
6. 자격 증명이 유효 만들기는 **IPrincipal** 설정 `context.Principal`합니다.

다음 코드에 나와 있는는 **AuthenticateAsync** 에서 메서드는 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플. 주석은 각 단계를 나타냅니다. 코드는 여러 유형의 오류를 보여 줍니다: 없고 자격 증명, 잘못 된 형식의 자격 증명이 잘못 된 사용자 이름/암호는 인증 헤더.

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>오류 결과 설정합니다.

필터는 자격 증명이 유효 하는 경우 설정 해야 `context.ErrorResult` 에 **IHttpActionResult** 를 만드는 오류 응답입니다. 에 대 한 자세한 내용은 **IHttpActionResult**, 참조 [Web API 2에 대 한 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.

기본 인증 샘플에 포함 되어는 `AuthenticationFailureResult` 이 목적을 위해 적합 한 클래스입니다.

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>ChallengeAsync 구현

용도 **ChallengeAsync** 방법은 필요한 경우 인증 챌린지를 응답에 추가 하는 것입니다. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

요청 파이프라인의 모든 인증 필터에 메서드가 호출 됩니다.

이러한 점을 이해 해야 **ChallengeAsync** 라고 *하기 전에* HTTP 응답을 만들고, 컨트롤러 동작 실행 하기 전에 합니다. 때 **ChallengeAsync** 호출 `context.Result` 포함는 **IHttpActionResult**, HTTP 응답을 만드는 나중에 사용 되는 합니다. 따라서 **ChallengeAsync** 는 호출을 알 수 없는 HTTP 응답에 대해 아직 합니다. **ChallengeAsync** 메서드의 원래 값을 대체 해야 `context.Result` 를 새 **IHttpActionResult**합니다. 이 **IHttpActionResult** 원래 래핑해야 `context.Result`합니다.

![](authentication-filters/_static/image3.png)

원래 이라고 부르겠습니다 **IHttpActionResult** 는 *내부 결과*와 새 **IHttpActionResult** 는 *외부 결과*합니다. 외부 결과 다음을 수행 해야 합니다.

1. HTTP 응답을 만드는 내부 결과 호출 합니다.
2. 응답을 검사 합니다.
3. 필요에 따라 인증 챌린지를 응답에 추가 합니다.

다음 예제에서는 기본 인증 샘플에서 가져옵니다. 정의 **IHttpActionResult** 외부 결과 대 한 합니다.

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` 속성 내부에 저장 **IHttpActionResult**합니다. `Challenge` 속성 Www 인증 헤더를 나타냅니다. 다음에 유의 **ExecuteAsync** 첫 번째로 호출 `InnerResult.ExecuteAsync` HTTP 응답을 만드는 다음 필요한 경우 챌린지를 추가 합니다.

챌린지를 추가 하기 전에 응답 코드를 확인 합니다. 대부분 인증 스키마에만 챌린지를 추가할 경우 응답 401을 다음과 같이 합니다. 그러나 일부 인증 스키마 성공 응답에 챌린지를 추가지 않습니다. 예를 들어 참조 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).

제공 된 `AddChallengeOnUnauthorizedResult` 클래스의 실제 코드 **ChallengeAsync** 은 간단 합니다. 방금 결과 만들어 하도록 `context.Result`합니다.

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

참고: 기본 인증 샘플 추상화이 논리 약간 확장 메서드에서 배치 하 여 합니다.

## <a name="combining-authentication-filters-with-host-level-authentication"></a>호스트 수준의 인증을 사용 하 여 인증 필터를 결합합니다.

"호스트 수준" 인증은 (예: IIS), 호스트에서 수행 하는 인증 요청에 도달 Web API 프레임 워크 하기 전에입니다.

종종 하려는 경우에 응용 프로그램의 나머지 부분에 대 한 호스트 수준 인증을 사용 하도록 설정 하지만 Web API 컨트롤러에 대 한 사용 하지 않도록 설정 합니다. 예를 들어 호스트 수준에서 폼 인증을 사용 하도록 설정 하지만 웹 API에 대 한 토큰 기반 인증을 사용 하는 일반적인 시나리오가입니다.

Web API 파이프라인 내 호스트 수준의 인증을 사용 하지 않으려면 호출 `config.SuppressHostPrincipal()` 구성에서 합니다. 이 인해 웹 API를 제거 하는 **IPrincipal** Web API 파이프라인이 입력 하는 모든 요청에서. 효과적으로 그 &quot;취소-인증&quot; 요청 합니다.

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 API 보안 필터가](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)
