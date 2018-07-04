---
uid: web-api/overview/security/integrated-windows-authentication
title: 통합 Windows 인증 | Microsoft Docs
author: MikeWasson
description: 통합 Windows 인증을 사용 하 여 ASP.NET Web API에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/18/2012
ms.topic: article
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: f11b9fe5d98118a252c6c00dd2997b2ee9a3da7a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381605"
---
<a name="integrated-windows-authentication"></a>통합된 Windows 인증
====================
[Mike Wasson](https://github.com/MikeWasson)

통합된 Windows 인증에 Kerberos 또는 NTLM을 사용 하는 Windows 자격 증명을 사용 하 여 로그인 할 수 있습니다. 클라이언트 자격 증명 권한 부여 헤더를 보냅니다. Windows 인증은 인트라넷 환경에 가장 적합 합니다. 자세한 내용은 [Windows 인증](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)합니다.

| 장점 | 단점 |
| --- | --- |
| -IIS에 빌드됩니다. -요청에 사용자 자격 증명을 보내지 않습니다. -클라이언트 컴퓨터는 도메인 (예를 들어 인트라넷 응용 프로그램)에 속하는 경우에 사용자를 자격 증명을 입력 하지 않아도 됩니다. | -인터넷 응용 프로그램에 권장 되지 않습니다. -클라이언트에서 Kerberos 또는 NTLM 지원이 필요합니다. 클라이언트는 Active Directory 도메인에 있어야 합니다. |

> [!NOTE]
> 응용 프로그램이 Azure에서 호스트 되 고에 온-프레미스 Active Directory 도메인에 있는 경우에 Azure Active Directory를 사용 하 여 온-프레미스 AD를 페더레이션 하는 것이 좋습니다. 이런 방식으로 사용자가 온-프레미스 자격 증명을 사용 하 여 기록할 수 있지만 Azure AD에서 인증을 수행 합니다. 자세한 내용은 [Azure 인증](../../../visual-studio/overview/2012/windows-azure-authentication.md)합니다.


통합 Windows 인증을 사용 하는 응용 프로그램을 만들려면 MVC 4 프로젝트 마법사에서 "인트라넷 응용 프로그램" 템플릿을 선택 합니다. 이 프로젝트 템플릿은 Web.config 파일에서 다음 설정을 설정합니다.

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

클라이언트 쪽에서 통합 Windows 인증을 지 원하는 모든 브라우저를 사용 하 여 작동 합니다 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 대부분의 주요 브라우저를 포함 하는 인증 체계입니다. .NET 클라이언트 응용 프로그램을 **HttpClient** 클래스는 Windows 인증을 지원 합니다.

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 인증은 교차 사이트 요청 위조 (CSRF) 공격에 취약 합니다. 참조 [교차 사이트 요청 위조 (CSRF) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.
