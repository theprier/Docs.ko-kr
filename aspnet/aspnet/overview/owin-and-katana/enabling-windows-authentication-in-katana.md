---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: "Katana에서 Windows 인증을 사용 하도록 설정 | Microsoft Docs"
author: MikeWasson
description: "이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 설명 합니다. 두 가지 시나리오를 다룹니다: Katana, 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 캐 탈 자체 호스트 하 고 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 8a26d356f7abafba021199761f9a49dcb81765c5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="enabling-windows-authentication-in-katana"></a>Katana에서 Windows 인증을 사용 하도록 설정
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 설명 합니다. 두 가지 시나리오를 다룹니다: Katana, 호스트에 IIS를 사용 하 고 HttpListener를 사용 하 여 사용자 지정 프로세스에서 Katana를 자체 호스트 합니다. 이 문서를 검토 하기 위한 Chris Ross Barry Dorrans, David Matson을 가져주셔서 감사 합니다.


Katana은 Microsoft에서 구현한 [OWIN](http://owin.org/),.NET에 대 한 열린 웹 인터페이스입니다. OWIN 및 Katana 소개를 읽을 수 [여기](an-overview-of-project-katana.md)합니다. OWIN 아키텍처에 대 한 여러 계층에 있습니다.

- 호스트: OWIN 파이프라인 실행 되는 프로세스를 관리 합니다.
- 서버: 네트워크 소켓을 열고 요청을 수신 합니다.
- 미들웨어: HTTP 요청 및 응답을 처리합니다.

Katana에는 현재 Windows 통합 인증을 모두 지 원하는 두 명의 서버를 제공 합니다.

- **Microsoft.Owin.Host.SystemWeb**. ASP.NET 파이프라인을 IIS를 사용합니다.
- **Microsoft.Owin.Host.HttpListener**. 사용 하 여 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)합니다. 자체 호스팅하는 경우이 서버는 현재 기본 옵션 Katana 합니다.

> [!NOTE]
> Katana 현재 제공 하지 않습니다 OWIN 미들웨어입니다. Windows 인증을 위해 서버에서이 기능을 이미 있으므로 합니다.


## <a name="windows-authentication-in-iis"></a>IIS에서 Windows 인증

Microsoft.Owin.Host.SystemWeb를 사용 하 여 단순히 IIS에서 Windows 인증을 사용할 수 있습니다.

새 ASP.NET 응용 프로그램 "ASP.NET 빈 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여를 만들어 보겠습니다.

![](enabling-windows-authentication-in-katana/_static/image1.png)

NuGet 패키지를 다음으로 추가 합니다. **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

즉 하기만 하면 IIS에서 실행 중인 OWIN에 대 한 "Hello world" 응용 프로그램을 만듭니다. F5 키를 눌러 응용 프로그램을 디버깅합니다. "Hello World!"이 표시 됩니다. 브라우저 창에서.

![](enabling-windows-authentication-in-katana/_static/image2.png)

다음으로, IIS Express에서 Windows 인증을 활성화 합니다. **보기** 메뉴 선택 **속성**합니다. 프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.

에 **속성** 창의 설정 **익명 인증** 를 **비활성화** 설정 **Windows 인증** 를  **활성화**합니다.

![](enabling-windows-authentication-in-katana/_static/image3.png)

Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express는 사용자의 Windows 자격 증명이 필요 합니다. 사용 하 여 볼 수 있습니다 [Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구입니다. HTTP 응답 예는 다음과 같습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

이 응답에 WWW 인증 헤더는 서버에서 지원 되는지 표시는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) Kerberos 또는 NTLM을 사용 하는 프로토콜입니다.

서버에 응용 프로그램을 배포 하는 경우에 따라 나중 [이러한 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 해당 서버에 IIS에서 Windows 인증을 사용할 수 있도록 합니다.

## <a name="windows-authentication-in-httplistener"></a>HttpListener에서 Windows 인증

직접 Windows 인증을 사용할 수 Microsoft.Owin.Host.HttpListener를 자체 Katana 호스트를 사용 하는 경우는 **HttpListener** 인스턴스.

먼저 새 콘솔 응용 프로그램을 만듭니다. NuGet 패키지를 다음으로 추가 합니다. **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

이제 라는 클래스를 추가 `Startup` 다음 코드를 사용 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

이전에 동일한 "Hello world" 예제에서이 클래스를 구현 하지만 인증 체계로 Windows 인증을 설정 합니다.

내에서 `Main` 함수, OWIN 파이프라인을 시작 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

응용 프로그램이 Windows 인증을 사용 하 고 있는지 확인 하는 Fiddler에서 요청을 보낼 수 있습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>관련 항목

[프로젝트 Katana 개요](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[MVC 5의에서 OWIN 폼 인증 이해](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
