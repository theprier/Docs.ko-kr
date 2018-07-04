---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET Web API에서에서 교차 사이트 요청 위조 (CSRF) 공격 방지 | Microsoft Docs
author: MikeWasson
description: 교차 사이트 요청 위조 (CSRF) 공격 및 ASP.NET Web API에서 CSRF 방지 조치를 구현 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 7dfddf09a1577cfa7a52f58b37533724a8475435
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379876"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a>ASP.NET Web API에서에서 교차 사이트 요청 위조 (CSRF) 공격 방지
====================
[Mike Wasson](https://github.com/MikeWasson)

교차 사이트 요청 위조 (CSRF) 공격 악성 사이트 여기서 사용자가 현재 로그인 한 취약 한 사이트에 요청을 보냅니다 하는 위치는

CSRF 공격의 예는 다음과 같습니다.

1. 사용자가 로그인 `www.example.com` 폼 인증을 사용 합니다.
2. 서버에서 사용자를 인증 합니다. 인증 쿠키를 포함 하는 서버에서 응답 합니다.
3. 로그 아웃을 하지 않고 사용자가 악성 웹 사이트를 방문 합니다. 다음 HTML 양식을 포함 하는이 악성 사이트: 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Form action는 취약 한 사이트 악의적인 사이트에 게시 하는 확인 합니다. CSRF의 "교차 사이트" 부분입니다.
4. 제출 단추를 클릭 합니다. 브라우저 요청을 사용 하 여 인증 쿠키를 포함합니다.
5. 요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되 고 인증된 된 사용자가 수행할 수 있는 아무 것도 가능 합니다.

이 예제에서는 사용자가 폼 단추 클릭, 되지만 폼을 자동으로 전송 하는 스크립트를 실행 하는 쉽게와 마찬가지로 악의적인 페이지 수 없습니다. 또한 악성 사이트 "https://" 요청을 보낼 수 있기 때문에 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.

일반적으로 CSRF 공격은 인증용 쿠키를 사용 하는 웹 사이트에 대해 가능한 브라우저 대상 웹 사이트에 모든 관련 쿠키를 보낼 수 없기 때문입니다. 그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다. 예를 들어, 기본 및 다이제스트 인증은 또한 취약 합니다. 이후에 사용자가 기본 또는 다이제스트 인증을 사용 하 여 로그인 합니다. 브라우저는 세션이 종료 될 때까지 자격 증명을 자동으로 보냅니다.

## <a name="anti-forgery-tokens"></a>위조 방지 토큰

CSRF 공격을 방지 하기 위해 ASP.NET MVC 위해 위조 방지 토큰을 라고도 *요청 확인 토큰*합니다.

1. 클라이언트는 양식을 포함 하는 HTML 페이지를 요청 합니다.
2. 서버 응답에서 두 개의 토큰을 포함합니다. 하나의 토큰은 쿠키로 전송 됩니다. 다른 숨겨진된 폼 필드에 배치 됩니다. 악의적 사용자가 값을 예상할 수 있도록 토큰을 임의로 생성 됩니다.
3. 클라이언트가 폼을 제출 하면 서버에 두 토큰이 모두 보내야 합니다. 클라이언트는 쿠키 토큰을 쿠키로 보내고 양식 데이터 내에서 폼 토큰을 보냅니다. (브라우저 클라이언트가 자동으로 수행이 사용자가 폼을 전송 합니다.)
4. 요청에 토큰이 모두 포함 되어 있지 않으면, 서버 요청을 허용 하지 않습니다.

숨겨진된 폼 토큰을 사용 하 여 HTML 폼의 예는 다음과 같습니다.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

위조 방지 토큰에는 악의적인 페이지 동일 원본 정책으로 인해 사용자의 토큰을 읽을 수 없으므로 작동 합니다. ([동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) 서로 콘텐츠를 액세스 하지 못하도록 하는 두 개의 다른 사이트에 호스트 된 문서를 방지 합니다. 따라서 이전 예제에서는 악의적인 페이지 요청을 보낼 수 example.com, 있지만 응답 읽을 수 없습니다.)

CSRF 공격 방지, 브라우저를 자동으로 보내는 모든 인증 프로토콜을 사용 하 여 위조 방지 토큰을 사용 하 여 사용자가 로그인 한 후 자격 증명입니다. 이 폼 인증과 같은 쿠키 기반 인증 프로토콜을 포함 합니다. 뿐만 아니라 기본 및 다이제스트 인증과 같은 프로토콜입니다.

Nonsafe 메서드 (POST, PUT, DELETE)에 대 한 위조 방지 토큰을 요청 해야 합니다. 또한 안전한 메서드 (GET, HEAD) 모든 파생 작업이 없는 해야 합니다. 또한 JSONP 또는 CORS와 같은 도메인 간 지원을 사용 하도록 설정 하면 다음 GET 등의 더 안전한 방법을 잠재적으로 취약할 CSRF 공격에 공격자가 잠재적으로 중요 한 데이터를 읽을 수 있도록 합니다.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC에서 위조 방지 토큰

Razor 페이지에 위조 방지 토큰을 추가 하려면 사용 합니다 **HtmlHelper.AntiForgeryToken** 도우미 메서드입니다.

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

이 메서드는 숨겨진된 폼 필드를 추가 하 고 쿠키 토큰을 설정 합니다.

## <a name="anti-csrf-and-ajax"></a>CSRF 방지 및 AJAX

AJAX 요청이 HTML 양식 데이터가 아닌 JSON 데이터를 보낼 수 있으므로 폼 토큰에서 AJAX 요청에 대 한 문제를 수 있습니다. 하나의 솔루션 사용자 지정 HTTP 헤더에 토큰을 보내는 것입니다. 다음 코드는 Razor 구문을 사용 하 여 토큰을 생성 하 고 AJAX 요청에 토큰을 추가 합니다. 토큰을 호출 하 여 서버에 생성 됩니다 **AntiForgery.GetTokens**합니다.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

요청을 처리 하는 경우 요청 헤더에서 토큰을 추출 합니다. 그런 다음 호출을 **AntiForgery.Validate** 토큰의 유효성을 검사 하는 방법입니다. 합니다 **유효성 검사** 메서드는 토큰이 유효 하지 않은 경우 예외를 throw 합니다.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
