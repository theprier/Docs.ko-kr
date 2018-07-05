---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 인증 (VB)를 Forms 인증으로 사용자 | Microsoft Docs
author: microsoft
description: '[Authorize] 특성을 사용 하는 방법을 알아봅니다 암호로 MVC 응용 프로그램의 특정 페이지를 보호 합니다. 관리 웹 사이트도 사용 하는 방법을 배웁니다.'
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: a9d55df3132a5b5ceeb49ed6d0b83b847f2f1e3b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828856"
---
<a name="authenticating-users-with-forms-authentication-vb"></a>폼 인증 (VB)를 사용 하 여 사용자 인증
====================
[Microsoft](https://github.com/microsoft)

> [Authorize] 특성을 사용 하는 방법을 알아봅니다 암호로 MVC 응용 프로그램의 특정 페이지를 보호 합니다. 사용자 및 역할 만들기 및 관리 하는 웹 사이트 관리 도구를 사용 하는 방법을 알아봅니다. 또한 사용자 계정 및 역할 정보를 저장 하는 위치를 구성 하는 방법에 알아봅니다.


이 자습서의 목표는 Forms를 사용 하는 방법을 설명 합니다. ASP.NET MVC 응용 프로그램에서 뷰를 보호 하는 암호를 인증 합니다. 사용자 및 역할을 만들려는 웹 사이트 관리 도구를 사용 하는 방법을 알아봅니다. 또한 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 하는 방법에 알아봅니다. 마지막으로, 사용자 이름 및 암호 저장 되는 위치를 구성 하는 방법에 알아봅니다.

#### <a name="using-the-web-site-administration-tool"></a>웹 사이트 관리 도구를 사용 하 여

다른 작업을 수행 하기 전에 일부 사용자 및 역할을 만들어 시작 해야 합니다. 새 사용자 및 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 활용 하는 경우 메뉴 옵션을 선택 하 여이 도구를 시작할 수 있습니다 **프로젝트를 ASP.NET 구성**합니다. 또는 솔루션 탐색기 창 위쪽에 표시 되는 전 세계에 도달 hammer의 (다소 scary) 아이콘을 클릭 하 여 웹 사이트 관리 도구를 시작할 수 있습니다 (그림 1 참조).

**그림 1-웹 사이트 관리 도구를 시작 합니다.**

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

웹 사이트 관리 도구에서 만든 새 사용자 및 역할 보안 탭을 선택 하 여 합니다. 클릭 합니다 **사용자 만들기** Stephen 라는 새 사용자를 만들려면 링크 (그림 2 참조). 원하는 모든 암호를 사용 하 여 Stephen 사용자 제공 (예를 들어 *비밀*).

**그림 2-새 사용자 만들기**

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

첫 번째 역할을 사용 하도록 설정 하 고 하나 이상의 역할을 정의 하 여 새 역할을 만듭니다. 클릭 하 여 역할을 활성화 합니다 **역할을 사용 하도록** 링크 합니다. 다음으로 명명 된 역할을 만듭니다 *관리자* 를 클릭 하 여는 **역할 만들기 또는 관리** 링크 (그림 3 참조).

**그림 3 – 새 역할 만들기**

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

마지막으로 Sally 라는 새 사용자를 만들고 사용자 만들기 링크를 클릭 하 고 Sally를 만들 때 관리자를 선택 하 여 Sally 관리자 역할과 연결 (그림 4 참조).

**그림 4 – 역할에 사용자 추가**

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

모두 수행 하 고, 경우에 Stephen 및 Sally 라는 두 개의 새 사용자가 해야 합니다. 또한 관리자 라는 새 역할을 하 고 있어야 합니다. Sally는 관리자 역할의 멤버 이며 Stephen 없습니다.

#### <a name="requiring-authorization"></a>권한 부여를 요구

사용자 작업에 [Authorize] 특성을 추가 하 여 컨트롤러 작업을 호출 하는 사용자 인증을 요구할 수 있습니다. 개별 컨트롤러 작업에 [Authorize] 특성을 적용할 수 있습니다 또는 전체 컨트롤러 클래스에이 특성을 적용할 수 있습니다.

예를 들어 목록 1에서 컨트롤러 CompanySecrets() 라는 작업을 노출 합니다. 이 작업은 [Authorize] 특성으로 데코 레이트 된,이 동작은 사용자가 인증 하지 않는 한 호출할 수 없습니다.

**1 – Controllers\HomeController.vb 나열**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

브라우저의 주소 표시줄에 URL /Home/CompanySecrets를 입력 하 여 CompanySecrets() 동작을 호출 하 고 인증된 된 사용자에 없는 경우 리디렉션됩니다 로그인 보기를 자동으로 (그림 5 참조).

**그림 5-로그인 보기**

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

사용자 이름 및 암호를 입력할 로그인 보기를 사용할 수 있습니다. 등록된 된 사용자 없는 경우 클릭할 수는 **등록** 등록으로 이동 하는 링크 (그림 6 참조)를 확인 합니다. 새 사용자 계정을 만들려면 레지스터 보기를 사용할 수 있습니다.

**그림 6 – 레지스터 보기**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

성공적으로 로그인 한 후 (그림 7 참조)을 보려면 CompanySecrets 볼 수 있습니다. 기본적으로 브라우저 창의 닫을 때까지 로그인 할 계속 됩니다.

**그림 7-CompanySecrets 보기**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>사용자 이름 또는 사용자 역할 권한 부여

사용자 또는 사용자 역할의 특정 집합의 특정 집합에 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용할 수 있습니다. 예를 들어 목록 2에서 수정 된 홈 컨트롤러 StephenSecrets() 및 AdministratorSecrets() 라는 두 가지 새 작업을 포함 합니다.

**Listing 2 – Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

Stephen 사용자 이름의 사용자만 StephenSecrets() 동작을 호출할 수 있습니다. 다른 모든 사용자가 로그인 뷰로 리디렉션됩니다. 사용자 속성에는 사용자 계정 이름의 쉼표로 구분 된 목록을 허용합니다.

관리자 역할의 사용자만 AdministratorSecrets() 동작을 호출할 수 있습니다. 예를 들어 Sally Administrators 그룹의 구성원 이므로 AdministratorSecrets() 작업을 호출할 수 그녀 합니다. 다른 모든 사용자가 로그인 뷰로 리디렉션됩니다. 역할 속성에는 역할 이름의 쉼표로 구분 된 목록을 허용합니다.

#### <a name="configuring-authentication"></a>인증 구성

이 시점에서 궁금할 사용자 계정 및 역할 정보가 저장 되는 위치입니다. MVC 응용 프로그램의 앱에 있는 명명 된 ASPNETDB.mdf (RANU) SQL Express 데이터베이스에 저장 하는 정보를 기본적으로\_데이터 폴더. 이 데이터베이스 멤버 자격을 사용 하기 시작할 때 ASP.NET 프레임 워크에 의해 생성 됩니다.

솔루션 탐색기 창에서 ASPNETDB.mdf 데이터베이스를 표시 하려면 먼저 메뉴 옵션을 프로젝트에 모든 파일 표시를 선택 해야 합니다.

기본 SQL Express 데이터베이스를 사용 하 여 응용 프로그램을 개발할 때 괜찮습니다. 그러나 대부분의 경우 없습니다 하려는 프로덕션 응용 프로그램에 대 한 기본 ASPNETDB.mdf 데이터베이스를 사용 합니다. 이 경우 다음 두 단계를 완료 하 여 사용자 계정 정보가 저장 되는 위치를 변경할 수 있습니다.

1. 프로덕션 데이터베이스에 응용 프로그램 서비스 데이터베이스 개체를 추가-프로덕션 데이터베이스를 가리키도록 응용 프로그램 연결 문자열 변경

첫 번째 단계 프로덕션 데이터베이스의 모든 필요한 데이터베이스 개체 (테이블 및 저장된 프로시저)를 추가 하는 것입니다. 새 데이터베이스에 이러한 개체를 추가 하는 가장 쉬운 방법은 ASP.NET SQL Server 설치 마법사를 활용 하는 것 (그림 8 참조). Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 열고 명령 프롬프트에서 다음 명령을 실행 하 여이 도구를 시작할 수 있습니다.

aspnet\_regsql

**그림 8 – ASP.NET SQL Server 설치 마법사**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL Server 설치 마법사를 사용 하면 네트워크에서 SQL Server 데이터베이스를 선택 하 고 ASP.NET 응용 프로그램 서비스에 필요한 데이터베이스 개체를 모두 설치할 수 있습니다. 데이터베이스 서버에 로컬 컴퓨터에 필요 하지 않습니다.

> [!NOTE]
> ASP.NET SQL Server 설치 마법사를 사용 하지 않으려는 경우 다음 폴더에 추가 하는 응용 프로그램 서비스 데이터베이스 개체에 대 한 SQL 스크립트를 찾을 수 있습니다.
> 
> 
> C:\Windows\Microsoft.NET\Framework\v2.0.50727


필요한 데이터베이스 개체를 만든 후에 MVC 응용 프로그램에서 사용 하 여 데이터베이스 연결을 수정 해야 합니다. 프로덕션 데이터베이스를 가리키도록 웹 구성 (web.config) 파일에서 ApplicationServices 연결 문자열을 수정 합니다. 예를 들어 목록 3에서 수정 된 연결 (원래 ApplicationServices 연결 문자열을 주석 처리 된) MyProductionDB 라는 데이터베이스를 가리킵니다.

**3 – Web.config를 나열합니다.**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>데이터베이스 사용 권한 구성

통합 보안을 사용 하 여 데이터베이스에 연결할 경우 데이터베이스에 로그인으로 올바른 Windows 사용자 계정을 추가 해야 됩니다. 올바른 계정을 웹 서버로 ASP.NET Development Server 또는 인터넷 정보 서비스 사용 중인지 여부에 따라 달라 집니다. 또한 올바른 사용자 계정 운영 체제에 따라 달라 집니다.

ASP.NET Development Server (Visual Studio에서 사용 된 기본 웹 서버)를 사용 하는 응용 프로그램의 Windows 사용자 계정의 컨텍스트 내에서 실행 합니다. 이 경우 데이터베이스 서버 로그인으로 Windows 사용자 계정을 추가 해야 합니다.

또는 인터넷 정보 서비스를 사용 하는 경우 다음 해야 데이터베이스 서버 로그인으로 ASPNET 계정 또는 NT AUTHORITY/NETWORK SERVICE 계정을 추가 합니다. Windows XP를 사용 하는 다음 데이터베이스에 로그인으로 ASPNET 계정을 추가 합니다. Windows Vista 또는 Windows Server 2008 등 최신 운영 체제를 사용 하는 경우 데이터베이스 로그인으로 다음 NT AUTHORITY/NETWORK SERVICE 계정을 추가 합니다.

Microsoft SQL Server Management Studio를 사용 하 여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다 (그림 9 참조).

**그림 9-새 Microsoft SQL Server 로그인 만들기**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

필요한 로그인을 만든 후 올바른 데이터베이스 역할을 사용 하 여 데이터베이스 사용자 로그인에 매핑할 필요 합니다. 로그인을 두 번 클릭 하 고 사용자 매핑 탭을 선택 합니다. 하나 이상의 응용 프로그램 서비스 데이터베이스 역할을 선택 합니다. 예를 들어, 사용자를 인증 하기 위해 사용 하도록 설정 해야 aspnet\_멤버 자격\_BasicAccess 데이터베이스 역할. 새 사용자를 만들기 위해 aspnet를 사용 하도록 설정 해야\_멤버 자격\_FullAccess 데이터베이스 역할 (그림 10 참조).

**그림 10-응용 프로그램 서비스 데이터베이스 역할 추가**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드할 때 폼 인증을 사용 하는 방법을 알아보았습니다. 첫째, 웹 사이트 관리 도구를 활용 하 여 새 사용자 및 역할을 만드는 방법을 알아보았습니다. 다음으로, 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 [Authorize] 특성을 사용 하는 방법을 알아보았습니다. 마지막으로, 프로덕션 데이터베이스에서 사용자 및 역할 정보를 저장 하는 MVC 응용 프로그램을 구성 하는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [이전](preventing-javascript-injection-attacks-cs.md)
> [다음](authenticating-users-with-windows-authentication-vb.md)
