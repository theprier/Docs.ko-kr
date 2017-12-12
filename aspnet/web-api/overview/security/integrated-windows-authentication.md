---
uid: web-api/overview/security/integrated-windows-authentication
title: "Windows 통합 인증을 | Microsoft Docs"
author: MikeWasson
description: "Windows 통합 인증을 사용 하 여 ASP.NET Web API에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/18/2012
ms.topic: article
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: bf5f55d98d61cdfdd246a847f41a6f1c65f00bfc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="integrated-windows-authentication"></a>Windows 통합된 인증
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

통합된 Windows 인증에 사용자가 Kerberos 또는 NTLM을 사용 하 여 Windows 자격 증명으로 로그인 할 수 있습니다. 클라이언트 자격 증명을 인증 헤더에 보냅니다. Windows 인증은 인트라넷 환경에 가장 적합 합니다. 자세한 내용은 참조 [Windows 인증](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)합니다.

| 장점 | 단점 |
| --- | --- |
| -IIS 기본 제공 됩니다. -요청에 사용자 자격 증명을 보내지 않습니다. -클라이언트 컴퓨터에 도메인 (예를 들어 인트라넷 응용 프로그램)에 속한 경우 사용자가 자격 증명을 입력할 필요가 없습니다. | -인터넷 응용 프로그램에 대 한 권장 되지 않습니다. -클라이언트의 Kerberos 또는 NTLM 지원이 필요합니다. 클라이언트는 Active Directory 도메인에 있어야 합니다. |

> [!NOTE]
> 응용 프로그램은 Azure에서 호스트 되 고 온-프레미스 Active Directory 도메인에 있는 경우에 Azure Active Directory와 온-프레미스 AD를 페더레이션 하는 것이 좋습니다. 이런 방식으로 사용자가 자신의 온-프레미스 자격 증명을 사용 하 여 로그온 수 있지만 Azure AD에서 인증이 수행 됩니다. 자세한 내용은 참조 [Azure 인증](../../../visual-studio/overview/2012/windows-azure-authentication.md)합니다.


Windows 통합 인증을 사용 하는 응용 프로그램을 만들려면 "인트라넷 응용 프로그램" 템플릿은 MVC 4 프로젝트 마법사에서 선택 합니다. 이 프로젝트 템플릿은 Web.config 파일에서 다음 설정을 설정합니다.

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

클라이언트 쪽에서 Windows 통합 인증을 지 원하는 모든 브라우저 작동는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 대부분의 주요 브라우저를 포함 하는 인증 체계입니다. .NET 클라이언트 응용 프로그램에 대 한는 **HttpClient** 클래스는 Windows 인증을 지원 합니다.

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 인증은 교차 사이트 요청 위조 (CSRF) 공격에 취약 합니다. 참조 [교차 사이트 요청 위조 (CSRF) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.
