---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana에서 Windows 인증을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: '이 문서에서는 Katana에서 Windows 인증을 사용 하는 방법을 보여 줍니다. 두 가지 시나리오를 다룹니다: Katana 호스트에 IIS를 사용 하 여 및 자체 호스트 하는 캐 탈 HttpListener를 사용 하는 중...'
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 80bdc3c76c8867dc559e80a794ac8bee84b47646
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826328"
---
<a name="enabling-windows-authentication-in-katana"></a>Katana에서 Windows 인증 사용
====================
[Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 Katana에서 Windows 인증을 사용 하는 방법을 보여 줍니다. 두 가지 시나리오를 다룹니다: Katana 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 자체 사용자 지정 프로세스에서 Katana를 호스트 하는 합니다. Barry Dorrans, David Matson Chris Ross를이 문서를 검토에 참여해 주셔서 감사 합니다.


Katana는 Microsoft에서 구현한 [OWIN](http://owin.org/), Open Web Interface for.NET. OWIN 및 Katana 소개를 읽어보세요 [여기](an-overview-of-project-katana.md)합니다. OWIN 아키텍처에는 여러 계층에 있습니다.

- 호스트: OWIN 파이프라인을 실행 하는 프로세스를 관리 합니다.
- 서버: 네트워크 소켓을 열고 요청을 수신 합니다.
- 미들웨어: HTTP 요청 및 응답을 처리합니다.

Katana에는 현재 Windows 통합 인증을 모두 지 원하는 두 서버를 제공 합니다.

- **Microsoft.Owin.Host.SystemWeb**. ASP.NET 파이프라인을 사용 하 여 IIS를 사용합니다.
- **Microsoft.Owin.Host.HttpListener**. 사용 하 여 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)합니다. 자체 호스팅하는 경우이 서버는 현재 기본 옵션 Katana 합니다.

> [!NOTE]
> Katana 제공 하지 않습니다 현재 OWIN 미들웨어입니다. Windows 인증을 위해 때문이 기능은 이미 서버에 사용할 수 있습니다.


## <a name="windows-authentication-in-iis"></a>IIS에서 Windows 인증

Microsoft.Owin.Host.SystemWeb를 사용 하 여 IIS에서 Windows 인증 간단히 설정할 수 있습니다.

새 ASP.NET 응용 프로그램을 만들어, "ASP.NET 빈 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 시작 해 보겠습니다.

![](enabling-windows-authentication-in-katana/_static/image1.png)

그런 다음 NuGet 패키지를 추가 합니다. **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 하 여:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

이것이 전부 owin을 IIS에서 실행 되는 "Hello world" 응용 프로그램을 만들어야 합니다. F5 키를 눌러 응용 프로그램을 디버깅합니다. "Hello World!" 표시 브라우저 창에서.

![](enabling-windows-authentication-in-katana/_static/image2.png)

다음으로, IIS Express에서 Windows 인증을 지원할 예정입니다. **뷰** 메뉴에서 **속성**합니다. 프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.

에 **속성** 창에서 **익명 인증** 에 **사용 안 함** 설정 하 고 **Windows 인증** 를  **사용 하도록 설정**합니다.

![](enabling-windows-authentication-in-katana/_static/image3.png)

Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express는 사용자의 Windows 자격 증명이 필요 합니다. 사용 하 여이 확인할 수 있습니다 [Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구입니다. HTTP 응답 예제는 다음과 같습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

이 응답에 Www-authenticate 헤더를 서버에서 지원 되는지 나타냅니다 합니다 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) Kerberos 또는 NTLM을 사용 하는 프로토콜입니다.

서버에 응용 프로그램을 배포한 경우에 따라 나중 [이 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 해당 서버의 IIS에서 Windows 인증을 사용 하도록 설정 합니다.

## <a name="windows-authentication-in-httplistener"></a>HttpListener에서 Windows 인증

Microsoft.Owin.Host.HttpListener Katana를 자체 호스트를 사용 하는 경우에 직접 Windows 인증을 사용할 수 있습니다 합니다 **HttpListener** 인스턴스.

먼저 새 콘솔 응용 프로그램을 만듭니다. 그런 다음 NuGet 패키지를 추가 합니다. **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 하 여:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

이 클래스는 이전에 동일한 "Hello world" 예제에서 구현 되지만 인증 체계로 한 Windows 인증을 설정 합니다.

내부는 `Main` 함수, OWIN 파이프라인을 시작 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

응용 프로그램이 Windows 인증을 사용 하 고 있음을 확인 하는 Fiddler에서 요청을 보낼 수 있습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>관련 항목

[프로젝트 Katana 개요](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[MVC 5의에서 OWIN Forms 인증 이해](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
