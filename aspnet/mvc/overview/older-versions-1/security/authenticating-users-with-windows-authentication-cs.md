---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Windows 인증 (C#)을 사용 하는 사용자를 인증 | Microsoft Docs
author: microsoft
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다. 응용 프로그램의 웹 co 내에서 Windows 인증을 사용 하도록 설정 하는 방법을 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 140d2232f7826e178301d1d2064e12657be23385
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875385"
---
<a name="authenticating-users-with-windows-authentication-c"></a>Windows 인증 (C#)을 사용 하는 사용자 인증
====================
by [Microsoft](https://github.com/microsoft)

> MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다. Iis 인증을 구성 하는 방법 및 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법을 설명 합니다. 마지막으로, 특정 Windows 사용자 또는 그룹에 있는 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용 하는 방법을 배웁니다.


이 자습서의 목표 있습니다 사용할 수 있는 방법을 설명 하는 보안의 암호로 인터넷 정보 서비스에 기본 제공 하는 기능을 MVC 응용 프로그램에서 뷰를 보호 합니다. 특정 Windows 사용자 또는 특정 Windows 그룹의 구성원 인 사용자만 하 여 호출할 컨트롤러 작업을 허용 하는 방법을 배웁니다.

Windows 인증을 사용 하 여 있을 때 의미가 내부 회사 웹 사이트 (인트라넷 사이트)를 작성 하는 중이 고 웹 사이트에 액세스할 때의 표준 Windows 사용자 이름 및 암호를 사용할 수 있도록 합니다. 웹 사이트 (한 인터넷 웹 사이트)을 바라보는 바깥쪽을 작성 하는 경우에 대신 폼 인증을 사용 하는 것이 좋습니다.

#### <a name="enabling-windows-authentication"></a>Windows 인증을 사용 하도록 설정

새 ASP.NET MVC 응용 프로그램을 만들 때 Windows 인증이 기본적으로 사용 되지 않습니다. 폼 인증은 기본 인증 형식은 MVC 응용 프로그램에 대해 사용 하도록 설정 합니다. MVC 응용 프로그램의 웹 구성 파일 (web.config) 파일을 수정 하 여 Windows 인증을 활성화 해야 합니다. 찾을 &lt;인증&gt; 섹션 및 다음과 같은 폼 인증 대신 Windows를 사용 하도록 수정 합니다.

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Windows 인증을 사용 하도록 설정 하면 웹 서버는 사용자를 인증에 대 한 책임을 집니다. 일반적으로 두 가지 유형의 만들기 및 ASP.NET MVC 응용 프로그램 배포 시 사용 하는 웹 서버 있습니다.

먼저, MVC 응용 프로그램을 개발 하는 동안 사용 하 여 Visual Studio에 포함 된 ASP.NET 개발 웹 서버입니다. 기본적으로 ASP.NET 개발 웹 서버는 현재 Windows 계정 (Windows에 로그인 할 때 사용한 계정 모두)의 컨텍스트에서 모든 페이지를 실행 합니다.

ASP.NET 개발 웹 서버는 NTLM 인증도 지원합니다. 솔루션 탐색기 창에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 하 여 NTLM 인증을 사용할 수 있습니다. 그런 다음 웹 탭을 선택 하 고 NTLM 확인란 (그림 1 참조).

**그림 1-사용 하도록 설정 하면 ASP.NET 개발 웹 서버에 대 한 NTLM 인증**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

프로덕션 웹 응용 프로그램에 대 한는 한편 있습니다 IIS에 웹 서버로 사용합니다. IIS는 여러 형식을 포함 하 여 인증을 지원합니다.

- 기본 인증-HTTP 1.0 프로토콜의 일부로 정의 합니다. 사용자 이름 및 암호를 일반 텍스트로 (Base64 인코딩) 인터넷을 통해 보냅니다. 다이제스트 인증 – 자체는 인터넷을 통해 암호 대신 암호의 해시를 보냅니다. -통합된 Windows (NTLM) 인증-가장 적합 한 기간을 사용 하는 인트라넷 환경에서 사용할 인증 종류입니다. -인증서 인증-클라이언트 인증서를 사용 하 여 사용 하면 인증 합니다. 인증서는 Windows 사용자 계정에 매핑됩니다.

> [!NOTE] 
> 
> 이러한 유형의 인증의 보다 자세한 개요를 참조 하십시오. [ https://msdn.microsoft.com/library/aa292114(VS.71).aspx ](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)합니다.


특정 유형의 인증을 사용 하도록 설정 하려면 인터넷 정보 서비스 관리자를 사용할 수 있습니다. 주의 모든 종류의 인증은 모든 운영 체제의 경우 사용할 수 없습니다. 또한 Windows Vista와 함께 IIS 7.0을 사용할 경우에 인터넷 정보 서비스 관리자에 표시 하기 전에 다양 한 유형의 Windows 인증을 사용 하도록 설정 해야 합니다. 열기 **제어판, 프로그램, 프로그램 및 기능, Windows 기능 설정 또는 해제**, 인터넷 정보 서비스 노드를 확장 하 고 (그림 2 참조).

**그림 2 – 사용 하도록 설정 하면 Windows IIS 기능**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

인터넷 정보 서비스를 사용 하거나 설정할 수 있습니다 다른 종류의 인증을 사용 하지 않도록 설정 합니다. 예를 들어 그림 3에서는 익명 인증을 사용 하지 않도록 설정 하 고 통합 Windows (NTLM) 인증 사용 IIS 7.0을 사용 하는 경우

**그림 3 – Windows 통합된 인증을 사용 하도록 설정**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows 인증 사용자 및 그룹

Windows 인증을 사용 하도록 설정한 후에 컨트롤러 또는 컨트롤러 작업에 대 한 액세스를 제어 [Authorize] 특성을 사용할 수 있습니다. 이 특성은 전체 MVC 컨트롤러 또는 특정 컨트롤러 작업에 적용할 수 있습니다.

예를 들어 Home 컨트롤러 목록 1의 index (), CompanySecrets(), 및 StephenSecrets() 이라는 세 가지 동작을 노출 합니다. Index () 작업을 호출할 수 누구나 합니다. 그러나 Windows 로컬 관리자 그룹의 구성원만 CompanySecrets() 동작을 호출할 수 있습니다. 마지막으로, Stephen (Redmond 도메인)의 명명 된 Windows 도메인 사용자 StephenSecrets() 동작을 호출할 수 있습니다.

**1 – Controllers\HomeController.cs 나열**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> 때문에 Windows 컨트롤 UAC (사용자 계정), Windows Vista 또는 Windows Server 2008과 함께 작업 하는 경우, 로컬 관리자 그룹 다른 그룹 다르게 작동 됩니다. [Authorize] 특성 인식 하지 못합니다 올바르게 로컬 관리자 그룹의 구성원 컴퓨터의 UAC 설정을 수정 하지 않는 한 합니다.


정확 하 게 하는 경우 적절 한 사용 권한이 없지만 컨트롤러 작업을 호출 하려고 하면 활성화 되는 인증의 유형에 따라 달라 집니다. 기본적으로 ASP.NET 개발 서버를 사용 하는 경우, 단순히 빈 페이지를 가져옵니다. 페이지가으로 반환 되는 **401 권한이 없습니다.** HTTP 응답 상태입니다.

반면에 IIS를 사용 하는 사용 하지 않도록 설정 익명 인증과 기본 인증만 사용 하도록 설정 된 경우 보호 되는 페이지를 요청할 때마다 확인 된 로그인 대화 계속 해 (그림 4 참조).

**그림 4-기본 인증 로그인 대화 상자**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>요약

이 자습서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법을 설명 합니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법과 iis 인증을 구성 하는 방법을 배웠습니다. 마지막으로, 특정 Windows 사용자 또는 그룹에 있는 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-forms-authentication-cs.md)
> [다음](preventing-javascript-injection-attacks-cs.md)
