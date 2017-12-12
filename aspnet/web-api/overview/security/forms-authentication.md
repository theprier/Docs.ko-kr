---
uid: web-api/overview/security/forms-authentication
title: "ASP.NET Web API의에서 폼 인증 | Microsoft Docs"
author: MikeWasson
description: "폼 인증을 사용 하 여 ASP.NET Web API에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 9027d76bcf8854fc85f11906d3651511f350cd32
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API에서에서 폼 인증
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

폼 인증 HTML 폼을 사용 하 여 사용자의 자격 증명 서버에 보냅니다. 인터넷 표준 아닙니다. 폼 인증은 웹 응용 프로그램에서 호출 되는 web Api에 대 한 적절 한 사용자는 HTML 폼과 상호 작용할 수 있도록 합니다.

| 장점 | 단점 |
| --- | --- |
| -구현 하기 쉬운: ASP.NET에 기본 제공 합니다. -손쉽게 사용자 계정을 관리 하는 ASP.NET 멤버 자격 공급자를 사용 합니다. | --는 표준 HTTP 인증 메커니즘입니다. 표준 인증 헤더 대신 HTTP 쿠키를 사용합니다. -브라우저 클라이언트가 필요 합니다. -자격 증명은 텍스트로 전송 됩니다. -에 취약 교차 사이트 요청 위조 CSRF (); 앤티 CSRF 측정값이 필요합니다. -비 브라우저 클라이언트에서 사용 하기 어렵습니다. 로그인 하려면 브라우저를 필요 합니다. -사용자 자격 증명 요청에 전송 됩니다. -일부 사용자가 쿠키를 비활성화 합니다. |

간단히 말해서 asp.net에서 폼 인증은 다음과 같습니다.

1. 클라이언트 인증을 요구 하는 리소스를 요청 합니다.
2. 사용자 인증 되지 않은 경우 서버는 HTTP 302 (있음)를 반환 하 고 로그인 페이지로 리디렉션합니다.
3. 사용자 자격 증명을 입력 하 고 폼을 전송 합니다.
4. 서버는 원래 URI로 다시 리디렉션하는 다른 HTTP 302를 반환 합니다. 이 응답 하면 인증 쿠키가 포함 됩니다.
5. 클라이언트에서 리소스를 다시 요청 합니다. 서버 요청을 부여 하므로 인증 쿠키를 포함 하는 요청입니다.

![](forms-authentication/_static/image1.png)

자세한 내용은 참조 [는 폼 인증 개요입니다.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>폼 인증을 사용 하 여 web API

폼 인증을 사용 하는 응용 프로그램을 만들려면 "인터넷 응용 프로그램" 템플릿은 MVC 4 프로젝트 마법사에서 선택 합니다. 이 템플릿은 계정 관리에 대 한 MVC 컨트롤러를 만듭니다. 또한 ASP.NET Fall 2012 업데이트에서 사용할 수 있는 "단일 페이지 응용 프로그램" 서식 파일을 사용할 수 있습니다.

web API 컨트롤러를 사용 하 여 액세스를 제한할 수는 `[Authorize]` 특성에 설명 된 대로 [[Authorize] 특성을 사용 하 여](authentication-and-authorization-in-aspnet-web-api.md#auth3)합니다.

폼 인증 요청을 인증 하는 세션 쿠키를 사용 합니다. 브라우저가 자동으로 대상 웹 사이트에 모든 관련 쿠키를 전송 합니다. 이 기능을 사용 하면 폼 인증 교차 사이트 요청 위조 (CSRF) 참조 공격에 취약할 수 [방지 교차 사이트 요청 위조 CSRF () 공격](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.

폼 인증에서 사용자의 자격 증명을 암호화 하지 않습니다. 따라서 폼 인증 ssl을 사용 하지 않는 경우에 안전 하지 않습니다. 참조 [Web API의에서 SSL 작업](working-with-ssl-in-web-api.md)합니다.
