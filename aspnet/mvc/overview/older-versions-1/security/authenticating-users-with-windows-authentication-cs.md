---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Windows 인증 (C#)를 사용 하 여 사용자 인증 | Microsoft Docs
author: microsoft
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다. 응용 프로그램의 웹 co 내에서 Windows 인증을 사용 하는 방법에 알아봅니다...
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: dd5cea6b23aad668307326a46db91d8ee5526dcb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802077"
---
<a name="authenticating-users-with-windows-authentication-c"></a>Windows 인증 (C#)를 사용 하 여 사용자 인증
====================
[Microsoft](https://github.com/microsoft)

> MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 알아봅니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하는 방법 및 IIS를 사용 하 여 인증을 구성 하는 방법에 알아봅니다. 마지막으로, 특정 Windows 사용자나 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용 하는 방법에 알아봅니다.


이 자습서의 목표를 사용할 수 있는 방법을 설명 하는 보안의 기본 제공 기능에 인터넷 정보 서비스 암호로 보호 MVC 응용 프로그램의 보기입니다. 특정 Windows 사용자 또는 특정 Windows 그룹의 구성원 인 사용자에 의해서만 호출할 컨트롤러 작업을 허용 하는 방법에 알아봅니다.

Windows 인증을 사용 하 여 합리적 내부 회사 웹 사이트 (인트라넷 사이트)를 작성 하는 웹 사이트에 액세스할 때 해당 표준 Windows 사용자 이름과 암호를 사용할 수 있도록 하려는 경우입니다. 웹 사이트 (인터넷 웹 사이트를) 연결 하는 그라데이션이 작성 하는 경우에 폼 인증을 대신 사용 하는 것이 좋습니다.

#### <a name="enabling-windows-authentication"></a>Windows 인증을 사용 하도록 설정

새 ASP.NET MVC 응용 프로그램을 만들면 기본적으로 Windows 인증 사용 되지 않습니다. 폼 인증에는 MVC 응용 프로그램에 대 한 설정 기본 인증 유형입니다. MVC 응용 프로그램의 웹 구성 (web.config) 파일을 수정 하 여 Windows 인증을 사용 해야 합니다. 찾을 합니다 &lt;인증&gt; 섹션 및 다음과 같은 폼 인증 대신 Windows를 사용 하도록 수정 합니다.

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Windows 인증을 사용 하도록 설정 하면 웹 서버는 사용자를 인증 하는 것에 대 한 책임을 집니다. 일반적으로 웹 서버를 만들고 ASP.NET MVC 응용 프로그램을 배포할 때 사용 하는 두 가지 유형이 있습니다.

먼저 MVC 응용 프로그램을 개발 하는 동안 Visual Studio에 포함 된 ASP.NET 개발 웹 서버를 사용할 수 있습니다. 기본적으로 ASP.NET 개발 웹 서버는 현재 Windows 계정 (Windows에 로그온 할 때 사용한 모든 계정)의 컨텍스트에서 모든 페이지를 실행 합니다.

ASP.NET 개발 웹 서버에 NTLM 인증도 지원 합니다. 솔루션 탐색기 창에서 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 하 여 NTLM 인증을 사용할 수 있습니다. 다음으로, 웹 탭을 선택 하 고 NTLM 확인란 (그림 1 참조).

**그림 1-사용 하도록 설정 하면 ASP.NET 개발 웹 서버에 대 한 NTLM 인증**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

프로덕션 웹 응용 프로그램에 손 모양 아이콘이 있습니다 사용 하 여 IIS 웹 서버로 합니다. IIS 인증 등의 몇 가지 종류를 지원합니다.

- 기본 인증 – HTTP 1.0 프로토콜의 일부로 정의 합니다. 인터넷을 통해 일반 텍스트로 (Base64로 인코딩된) 사용자 이름 및 암호를 보냅니다. 다이제스트 인증 – 인터넷을 통해 자체 암호 대신 암호의 해시를 보냅니다. -통합형된 Windows (NTLM) 인증 – 가장 적합 한 유형의 windows를 사용 하 여 인트라넷 환경에서 사용할 인증입니다. -인증서 인증-클라이언트 쪽 인증서를 사용 하 여 수 있도록 인증 합니다. 인증서는 Windows 사용자 계정에 매핑합니다.

> [!NOTE] 
> 
> 이러한 서로 다른 유형의 인증의 자세한 개요를 참조 하세요 [ https://msdn.microsoft.com/library/aa292114(VS.71).aspx ](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)합니다.


특정 유형의 인증을 사용 하도록 설정 하려면 인터넷 정보 서비스 관리자를 사용할 수 있습니다. 모든 운영 체제의 경우 사용 가능한 모든 종류의 인증 되지 알아야 합니다. 또한 Windows Vista를 사용 하 여 IIS 7.0을 사용 중인 경우 인터넷 정보 서비스 관리자에 나타나기까지 다양 한 Windows 인증을 사용 하도록 설정 해야 합니다. 오픈 **제어판, 프로그램, 프로그램 및 기능을 설정 하는 Windows 기능 사용 /**, 인터넷 정보 서비스 노드를 확장 하 고 (그림 2 참조).

**그림 2 – 사용 하도록 설정 하면 Windows IIS 기능**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

인터넷 정보 서비스를 사용 하 여 사용 하도록 설정 수도 있고 서로 다른 유형의 인증을 사용 하지 않도록 설정할 수도 있습니다. 예를 들어 그림 3에서는 익명 인증을 사용 하지 않도록 설정 하 고 통합 Windows (NTLM) 인증을 사용 하도록 설정 하면 IIS 7.0을 사용 하는 경우

**그림 3-통합된 Windows 인증을 사용 하도록 설정**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows 인증 사용자 및 그룹

Windows 인증을 사용 하도록 설정한 후에 컨트롤러 또는 컨트롤러 작업에 대 한 액세스를 제어 하려면 [Authorize] 특성을 사용할 수 있습니다. 이 특성은 MVC 컨트롤러를 전체 또는 특정 컨트롤러 작업에 적용할 수 있습니다.

예를 들어 Home 컨트롤러 목록 1의 index (), CompanySecrets(), 및 StephenSecrets() 라는 세 가지 작업을 노출 합니다. Index () 작업을 호출할 수 누구나 합니다. 그러나 Windows 로컬 관리자 그룹의 구성원만 CompanySecrets() 동작을 호출할 수 있습니다. 마지막으로, Stephen (Redmond에) 라는 Windows 도메인 사용자만 StephenSecrets() 동작을 호출할 수 있습니다.

**1 – controllers\ homecontroller.cs를 나열합니다.**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> 인해 Windows 계정 컨트롤 (UAC (사용자), Windows Vista 또는 Windows Server 2008과 함께 작업 하는 경우, 로컬 관리자 그룹 다른 그룹 다르게 작동 합니다. 올바르게 [Authorize] 특성은 컴퓨터의 UAC 설정을 수정 하지 않는 한 로컬 관리자 그룹의 구성원을 인식 하지 못합니다.


정확 하 게 하는 경우 적절 한 권한이 없이 컨트롤러 작업을 호출 하려고 하면 사용 하도록 설정 하는 인증의 유형에 따라 달라 집니다. 기본적으로 ASP.NET Development Server를 사용 하는 경우, 단순히 빈 페이지가 나타납니다. 페이지가 사용 하 여 반환 되는 **401 권한이 없는** HTTP 응답 상태입니다.

다른 한편으로 사용 하지 않도록 설정 하는 익명 인증 및 사용 하도록 설정 하는 기본 인증을 사용 하 여 IIS를 사용 하는 경우 보호 되는 페이지를 요청할 때마다 로그인 대화 상자 프롬프트를 시작 유지 (그림 4 참조).

**그림 4-기본 인증 로그인 대화 상자**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>요약

이 자습서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법을 설명 합니다. IIS를 사용 하 여 인증을 구성 하는 방법과 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법을 배웠습니다. 마지막으로, 특정 Windows 사용자나 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-forms-authentication-cs.md)
> [다음](preventing-javascript-injection-attacks-cs.md)
