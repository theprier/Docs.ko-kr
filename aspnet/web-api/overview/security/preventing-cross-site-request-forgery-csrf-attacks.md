---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: "ASP.NET Web API의에서 교차 사이트 요청 위조 (CSRF) 공격 방지 | Microsoft Docs"
author: MikeWasson
description: "교차 사이트 요청 위조 (CSRF) 공격 및 앤티 CSRF 조치 ASP.NET Web API를 구현 하는 방법에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 1cd03f3b396cc2ece1d8dbe6820f6277c02d8e62
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a>ASP.NET Web API의에서 교차 사이트 요청 위조 (CSRF) 공격 방지
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

교차 사이트 요청 위조 CSRF ()은 악성 사이트를 사용자가 현재 로그인 취약 한 사이트에 요청을 보냅니다는 방식의 공격

CSRF 공격의 예는 다음과 같습니다.

1. Www.example.com에 사용자가 사용 하 여 폼 인증 합니다.
2. 서버에서 사용자를 인증 합니다. 서버 로부터 응답 하면 인증 쿠키가 포함 되어 있습니다.
3. 사용자 로그 아웃을 하지 않고 악성 웹 사이트를 방문 합니다. 이 악성 사이트 다음 HTML 폼을 포함 되어 있습니다. 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Form action에는 취약 한 사이트 악성 사이트에 게시 확인 합니다. CSRF의 "사이트 간" 부분입니다.
4. 사용자가 제출 단추를 클릭 합니다. 브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.
5. 요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되며 인증된 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.

하지만이 예제에서는 양식 단추를 클릭 하 여 사용자, 악의적인 페이지 것 처럼 쉽게 폼을 자동으로 전송 하는 스크립트를 실행할 수 있습니다. 또한 악성 사이트 "https://" 요청을 보낼 수 있으므로 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.

일반적으로 CSRF 공격은 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 전송 하기 때문에 인증을 위한 쿠키를 사용 하는 웹 사이트에 대해 가능한 합니다. 그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다. 예를 들어, 기본 및 다이제스트 인증 취약 됩니다. 기본 또는 다이제스트 인증을 사용 하 여 사용자가 있습니다. 브라우저는 세션이 종료 될 때까지 자격 증명을 자동으로 보냅니다.

## <a name="anti-forgery-tokens"></a>위조 방지 토큰

CSRF 공격을 방지 하려면 ASP.NET MVC에서 라고도 하는 위조 방지 토큰 사용 *확인 토큰을 요청할*합니다.

1. 클라이언트는 양식을 포함 하는 HTML 페이지를 요청 합니다.
2. 서버 응답에 두 개의 토큰을 포함합니다. 하나의 토큰은 쿠키로 전송 됩니다. 다른 숨겨진된 폼 필드에 배치 됩니다. 토큰은 악의적 사용자 값을 예상할 수 있도록 임의로 생성 됩니다.
3. 클라이언트 양식을 전송 하는 경우 서버에 다시 두 토큰이 보내야 합니다. 클라이언트는 쿠키 토큰을를 쿠키로 보내고 양식 데이터 내 폼 토큰을 보냅니다. (브라우저 클라이언트가 자동으로이 사용자가 폼을 제출 합니다.)
4. 요청에는 두 토큰이 포함 되어 있지 않으면, 서버 요청을 허용 하지 않습니다.

숨겨진된 폼 토큰을 사용 하 여 HTML 폼의 예는 다음과 같습니다.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

위조 방지 토큰에는 악의적인 페이지 동일 원본 정책으로 인해 사용자의 토큰을 읽을 수 없으므로 작동 합니다. ([동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) 다른 사용자의 내용에 액세스 하지 못하도록 하는 두 개의 다른 사이트에서 호스팅되는 문서를 방지 합니다. 따라서 앞의 예제에서 악의적인 페이지 요청을 보낼 수 example.com, 하지만 응답을 읽을 수 없습니다.)

CSRF 공격을 방지 브라우저가 자동으로 보내는 모든 인증 프로토콜 함께 위조 방지 토큰을 사용 하십시오 사용자가 로그인 한 후 자격 증명입니다. 이 같은 폼 인증 쿠키 기반 인증 프로토콜을 포함으로 기본 및 다이제스트 인증과 같은 프로토콜을 통해.

위조 방지 토큰 nonsafe 메서드 (POST, PUT, DELETE) 해야 합니다. 안전 메서드 (GET, HEAD) 모든 부작용을 포함 하지 않는지 확인 합니다. 또한 JSONP 또는 CORS와 같은 도메인 간 지원을 사용 하도록 설정 하면 다음도 안전 메서드 GET 같은 공격자가 잠재적으로 중요 한 데이터를 읽을 수 있도록 하는 CSRF 공격에 취약할 수입니다.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC에서 위조 방지 토큰

위조 방지 토큰에는 Razor 페이지를 추가 하려면 사용 하 여는 **HtmlHelper.AntiForgeryToken** 도우미 메서드입니다.

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

이 메서드는 숨겨진된 양식 필드를 추가 하 고 쿠키 토큰을 설정 합니다.

## <a name="anti-csrf-and-ajax"></a>앤티 CSRF 및 AJAX

AJAX 요청 JSON 데이터를 하지 HTML 폼 데이터를 보낼 수 있습니다 폼 토큰 AJAX 요청에 대 한 문제일 수 있습니다. 한 가지 해결 방법은 사용자 지정 HTTP 헤더에 토큰을 보내려고 합니다. 다음 코드에서는 Razor 구문을 사용 하 여 토큰을 생성 하 고 AJAX 요청에 토큰을 추가 합니다. 토큰은 호출 하 여 서버에 생성 된 **AntiForgery.GetTokens**합니다.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

요청을 처리 하는 경우 요청 헤더에서 토큰을 추출 합니다. 그런 다음 호출에서 **AntiForgery.Validate** 메서드는 토큰 유효성 검사를 합니다. **유효성 검사** 메서드 토큰이 유효 하지 않은 경우 예외를 throw 합니다.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
