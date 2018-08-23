---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API에서에서 기본 인증 | Microsoft Docs
author: MikeWasson
description: 기본 인증을 사용 하 여 ASP.NET Web API에 설명 합니다.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 7afafb6b7851f0d955d1f4292318f64d2a068a45
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838927"
---
<a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API에서에서 기본 인증
====================
[Mike Wasson](https://github.com/MikeWasson)

기본 인증에 정의 된 [RFC 2617, HTTP 인증: 기본 및 다이제스트 액세스 인증](http://www.ietf.org/rfc/rfc2617.txt)합니다.

단점

- 사용자 자격 증명 요청에 전송 됩니다.
- 자격 증명은 일반 텍스트로 전송 됩니다.
- 자격 증명은 모든 요청과 함께 전송 됩니다.
- 로그 아웃 하 수 없으므로 브라우저 세션을 종료 하 여 제외 합니다.
- 취약 하 게 교차 사이트 요청 위조 (CSRF); CSRF 방지 측정값이 필요합니다.

장점

- 인터넷 표준입니다.
- 모든 주요 브라우저에서 지원 합니다.
- 비교적 간단한 프로토콜입니다.

기본 인증 같이 작동합니다.

1. 요청에서 인증을 요구 하는 경우 서버는 401 (권한 없음)을 반환 합니다. 응답에 Www-authenticate 헤더를 나타내는 서버에서 기본 인증을 지원 합니다.
2. 클라이언트가 권한 부여 헤더에 있는 클라이언트 자격 증명을 사용 하 여 다른 요청을 보냅니다. 자격 증명 이름: "암호"를 base64로 인코딩된 문자열로 서식이 지정 됩니다. 자격 증명 암호화 되지 않습니다.

기본 인증 "영역입니다."의 컨텍스트 내에서 이루어집니다. Www-authenticate 헤더에 영역 이름을 포함 하는 서버입니다. 사용자의 자격 증명이 영역 안에서 사용할 수 있습니다. 정확한 영역 범위는 서버에서 정의 됩니다. 예를 들어 리소스를 분할 하는 순서 대로 여러 영역을 정의할 수 있습니다.

![](basic-authentication/_static/image1.png)

자격 증명은 암호화 되지 않은 전송 되므로, 기본 인증은 보안 https입니다. 참조 [Web API에서에서 SSL을 사용 하 여 작업](working-with-ssl-in-web-api.md)합니다.

기본 인증 CSRF 공격에 취약 이기도합니다. 사용자가 자격 증명을 입력 하면 브라우저 자동으로 보내 이후 요청에서 동일한 도메인에 세션 기간에 대 한 합니다. AJAX 요청이 포함 됩니다. 참조 [교차 사이트 요청 위조 (CSRF) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.

## <a name="basic-authentication-with-iis"></a>IIS 사용 하 여 기본 인증

IIS 기본 인증을 지원 하지만 주의할 점이: 사용자가 Windows 자격 증명에 대해 인증 됩니다. 즉, 사용자는 서버의 도메인에 계정이 있어야 합니다. 공용 웹 사이트의 경우 일반적으로 ASP.NET 멤버 자격 공급자에 대해 인증 하려고 합니다.

IIS를 사용 하 여 기본 인증을 사용 하려면 인증 모드를 ASP.NET 프로젝트의 Web.config에서 "Windows"로 설정 합니다.

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

이 모드에서 IIS 인증을 Windows 자격 증명을 사용 합니다. 또한 IIS에서 기본 인증을 활성화 해야 합니다. IIS 관리자에서 기능 보기로 이동 하 여 인증을 선택한 기본 인증을 사용 하도록 설정 합니다.

![](basic-authentication/_static/image2.png)

Web API 프로젝트에 추가 된 `[Authorize]` 인증 해야 하는 모든 컨트롤러 작업에 대 한 특성입니다.

클라이언트가 요청에서 권한 부여 헤더를 설정 하 여 자체 인증 합니다. 브라우저 클라이언트는 자동으로이 단계를 수행합니다. 비 브라우저 클라이언트 헤더를 설정 해야 합니다.

## <a name="basic-authentication-with-custom-membership"></a>사용자 지정 멤버 자격을 사용 하 여 기본 인증

언급 했 듯이 기본 인증을 IIS에 기본 제공 되는 Windows 자격 증명을 사용 합니다. 즉, 호스팅 서버에서 사용자에 대 한 계정을 만들어야 합니다. 하지만 인터넷 응용 프로그램 사용자 계정을 일반적으로 외부 데이터베이스에 저장 됩니다.

다음 코드는 HTTP 모듈은 기본 인증을 수행 하는 방법입니다. 대체 하 여 ASP.NET 멤버 자격 공급자에 쉽게 연결할 수 있습니다는 `CheckPassword` 메서드는이 예제에서 더미 메서드입니다.

Web API 2에서 쓰기를 고려해 야 하는 [인증 필터](authentication-filters.md) 또는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/index.md), HTTP 모듈을 대신 합니다.

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

HTTP 모듈을 사용 하려면 web.config 파일에 다음을 추가 합니다 **system.webServer** 섹션:

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

"이름을" ("dll" 확장명 포함 안 함) 어셈블리의 이름으로 바꿉니다.

Forms 또는 Windows 인증 등의 다른 인증 스키마를 사용 하지 않도록
