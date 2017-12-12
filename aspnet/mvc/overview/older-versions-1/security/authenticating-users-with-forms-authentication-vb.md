---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: "사용자를 인증 하는 것 폼 인증 (VB) | Microsoft Docs"
author: microsoft
description: "[Authorize] 특성을 사용 하는 방법에 알아봅니다 암호로 보호 하는 MVC 응용 프로그램의 특정 페이지입니다. 관리 웹 사이트도 사용 하는 방법을 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: c7d52e51158575c674264efd19c81de9b077d27b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="authenticating-users-with-forms-authentication-vb"></a>폼 인증 (VB)는 사용자 인증
====================
여 [Microsoft](https://github.com/microsoft)

> [Authorize] 특성을 사용 하는 방법에 알아봅니다 암호로 보호 하는 MVC 응용 프로그램의 특정 페이지입니다. 만들고 사용자 및 역할 관리 웹 사이트 관리 도구를 사용 하는 방법을 배웁니다. 또한 사용자 계정과 역할 정보를 저장 하는 구성 하는 방법을 알아봅니다.


이 자습서의 목표는 폼을 사용 하는 방법을 설명 하는 ASP.NET MVC 응용 프로그램에서 뷰를 보호 하는 암호를 인증 합니다. 사용자 및 역할을 만들려는 웹 사이트 관리 도구를 사용 하는 방법을 배웁니다. 또한 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하게 방지 하는 방법에 알아봅니다. 마지막으로, 사용자 이름 및 암호 저장 되는 위치를 구성 하는 방법을 배웁니다.

#### <a name="using-the-web-site-administration-tool"></a>웹 사이트 관리 도구를 사용 하 여

다른 작업을 수행 하기 전 일부 사용자 및 역할을 만들어 시작 해야 합니다. 새 사용자 및 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 활용 하는 합니다. 메뉴 옵션을 선택 하 여이 도구를 시작할 수 **프로젝트, ASP.NET 구성**합니다. 또는 솔루션 탐색기 창 위쪽에 표시 되는 전 세계에 도달 해머의 (다소 무시 무시) 아이콘을 클릭 하 여 웹 사이트 관리 도구를 시작할 수 있습니다 (그림 1 참조).

**그림 1-웹 사이트 관리 도구를 시작 합니다.**

![clip_image002 [4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

웹 사이트 관리 도구 내에서 만들면 새 사용자 및 역할 보안 탭을 선택 하 여 합니다. 클릭는 **사용자 만들기** Stephen 라는 새 사용자를 만들려면 링크 (그림 2 참조). Stephen 사용자에 게 모든 암호를 제공 (예를 들어 *비밀*).

**그림 2 – 새 사용자 만들기**

![clip_image004 [4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

역할을 활성화 한 다음 하나 이상의 역할을 정의 하 여 새 역할을 만듭니다. 클릭 하 여 역할을 사용 하도록 설정 된 **역할을 사용 하도록** 링크 합니다. 다음으로 명명 된 역할을 만들 *관리자* 클릭 하 여는 **역할 만들기 또는 관리** (그림 3 참조)를 연결 합니다.

**그림 3 –는 새 역할 만들기**

![clip_image006 [4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

마지막으로, Sally 라는 새 사용자를 만들고 사용자 만들기 링크를 클릭 하 고 Sally를 만들 때 관리자를 선택 하 여 관리자 역할 Sally 연결 (그림 4 참조).

**그림 4 – 역할에 사용자 추가**

![clip_image008 [4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

모두 수행 하 고 나면 때 Stephen 및 Sally 라는 두 개의 새 사용자가 있어야 합니다. 또한 관리자 라는 새 역할이 있어야 합니다. Sally 관리자 역할의 구성원 이므로 Stephen 없습니다.

#### <a name="requiring-authorization"></a>권한 부여를 요구

사용자 동작을 [Authorize] 특성을 추가 하 여 컨트롤러 작업을 호출 하는 사용자 인증을 요구할 수 있습니다. 개별 컨트롤러의 액션 [Authorize] 특성을 적용할 수 있습니다 또는 전체 컨트롤러 클래스에이 특성을 적용할 수 있습니다.

예를 들어 목록 1의 컨트롤러 CompanySecrets() 라는 동작을 노출 합니다. 이 작업은 [Authorize] 특성으로 데코레이팅, 사용자가 인증 하지 않는 한이 작업을 호출할 수 없습니다.

**1 – Controllers\HomeController.vb 나열**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

URL /Home/CompanySecrets 브라우저의 주소 표시줄에 입력 하 여 CompanySecrets() 작업을 호출 인증된 된 사용자에 없는 경우 자동으로 로그인 보기로 이동 될 합니다 (그림 5 참조).

**그림 5-로그인 보기**

![clip_image010 [4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

로그인 뷰를 사용 하 여 사용자 이름 및 암호를 입력할 수 있습니다. 등록 된 사용자 모를 경우 클릭할 수 있는 **등록** 링크 레지스터로 이동할 수 (그림 6 참조)를 확인 합니다. 레지스터 뷰를 사용 하 여 사용자 계정을 새로 만들 수 있습니다.

**그림 6 – 레지스터 보기**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

에 성공적으로 로그인 한 후 (그림 7 참조)를 보려면 CompanySecrets 볼 수 있습니다. 기본적으로 브라우저 창의 닫을 때까지 로그인 계속 됩니다.

**그림 7-CompanySecrets 보기**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>사용자 이름 또는 사용자 역할 권한 부여

사용자 또는 사용자 역할의 특정 집합의 특정 집합에는 컨트롤러 작업에 대 한 액세스를 제한 하려면 [Authorize] 특성을 사용할 수 있습니다. 예를 들어 목록 2의 수정 된 Home 컨트롤러 StephenSecrets() 및 AdministratorSecrets() 라는 두 개의 새 작업이 포함 되어 있습니다.

**2 – Controllers\HomeController.vb 나열**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

사용자 이름 Stephen 있는 사용자만 StephenSecrets() 동작을 호출할 수 있습니다. 다른 모든 사용자가 로그인 뷰로 이동 합니다. 사용자가 속성에는 사용자 계정 이름의 쉼표로 구분 된 목록을 허용합니다.

관리자 역할에 사용자만 AdministratorSecrets() 작업을 호출할 수 있습니다. 예를 들어 Sally Administrators 그룹의 구성원이 아니어서 AdministratorSecrets() 작업을 호출할 수 그녀. 다른 모든 사용자가 로그인 뷰로 이동 합니다. 역할 속성에는 역할 이름의 쉼표로 구분 된 목록을 허용합니다.

#### <a name="configuring-authentication"></a>인증 구성

이 시점에서 하는지에 대해 사용자 계정과 역할 정보를 저장 되는 위치입니다. 기본적으로 정보 MVC 응용 프로그램의 앱에 있는 명명 된 ASPNETDB.mdf (RANU) SQL Express 데이터베이스에 저장\_데이터 폴더. 이 데이터베이스 멤버 자격을 사용 하 여 시작 하는 경우 ASP.NET 프레임 워크에 의해 생성 됩니다.

솔루션 탐색기 창에서 ASPNETDB.mdf 데이터베이스를 보기 위해서는 먼저 모든 파일 표시 메뉴 옵션 프로젝트를 선택 해야 합니다.

응용 프로그램을 개발 하는 경우 기본 SQL Express 데이터베이스를 사용 하는 문제가 없습니다. 대부분의 경우, 없습니다 하려는 프로덕션 응용 프로그램에 대 한 기본 ASPNETDB.mdf 데이터베이스를 사용 합니다. 이 경우 다음 두 단계를 완료 하 여 사용자 계정 정보를 저장 하는 위치를 변경할 수 있습니다.

1. 프로덕션 데이터베이스 응용 프로그램 서비스 데이터베이스 개체를 추가-프로덕션 데이터베이스를 가리키도록 연결 문자열을 응용 프로그램 변경

첫 번째 단계 프로덕션 데이터베이스의 모든 필요한 데이터베이스 개체 (테이블 및 저장된 프로시저)를 추가 하는 것입니다. ASP.NET SQL Server 설치 마법사를 활용 하는 새 데이터베이스에 이러한 개체를 추가 하는 가장 쉬운 방법은 (그림 8 참조). Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 연 명령 프롬프트에서 다음 명령을 실행 하 여이 도구를 시작할 수 있습니다.

aspnet\_regsql

**그림 8 – ASP.NET SQL Server 설치 마법사**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL Server 설치 마법사를 사용 하면 네트워크에서 SQL Server 데이터베이스를 선택 하 고 ASP.NET 응용 프로그램 서비스에 필요한 데이터베이스 개체의 모든 설치 수 있습니다. 데이터베이스 서버 로컬 컴퓨터에 있는 것으로 필요 하지 않습니다.

> [!NOTE]
> ASP.NET SQL Server 설치 마법사를 사용 하지 않음 하는 경우 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가 하기 위한 SQL 스크립트를 찾을 수 있습니다.


> C:\Windows\Microsoft.NET\Framework\v2.0.50727


필요한 데이터베이스 개체를 만든 후에 MVC 응용 프로그램에서 사용 하는 데이터베이스 연결을 수정 해야 합니다. 프로덕션 데이터베이스를 가리키도록 웹 구성 파일 (web.config) 파일에서 ApplicationServices 연결 문자열을 수정 합니다. 예를 들어 목록 3에서 수정 된 연결 (원래 ApplicationServices 연결 문자열이 주석 처리 되었습니다) MyProductionDB 라는 데이터베이스를 가리킵니다.

**3 – Web.config를 나열합니다.**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>데이터베이스 사용 권한 구성

통합 보안을 사용 하 여 데이터베이스에 연결할 경우 데이터베이스에 로그인으로 올바른 Windows 사용자 계정을 추가 해야 합니다. 올바른 계정을 사용 여부는 ASP.NET 개발 서버 또는 인터넷 정보 서비스 웹 서버와에 따라 달라 집니다. 올바른 사용자 계정 운영 체제에 따라서도 다릅니다.

ASP.NET Development Server (Visual Studio에서 사용 되는 기본 웹 서버)를 사용 하는 응용 프로그램 Windows 사용자 계정의 컨텍스트 내에서 실행 합니다. 이 경우 데이터베이스 서버 로그인으로 Windows 사용자 계정을 추가 해야 합니다.

또는 인터넷 정보 서비스를 사용 하는 경우 다음 해야 데이터베이스 서버 로그인으로 ASPNET 계정 또는 NT 기관/네트워크 서비스 계정을 추가 합니다. Windows XP를 사용 하는 다음 데이터베이스에 로그인으로 ASPNET 계정을 추가 합니다. Windows Vista 또는 Windows Server 2008 같은 최신 운영 체제를 사용 하는 경우 NT 기관/네트워크 서비스 계정으로 데이터베이스 로그인을 추가 합니다.

Microsoft SQL Server Management Studio를 사용 하 여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다 (그림 9 참조).

**그림 9-새 Microsoft SQL Server 로그인 만들기**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

필요한 로그인을 만든 후 올바른 데이터베이스 역할을 가진 데이터베이스 사용자로 로그인을 매핑해야 할 합니다. 로그인을 두 번 클릭 하 고 사용자 매핑 탭을 선택 합니다. 하나 이상의 응용 프로그램 서비스 데이터베이스 역할을 선택 합니다. 예를 들어 사용자를 인증 하기 위해 있게 해야 aspnet\_구성원\_BasicAccess 데이터베이스 역할입니다. 새 사용자를 만들기 위해 aspnet를 사용 하도록 설정 해야\_구성원\_FullAccess 데이터베이스 역할 (그림 10 참조).

**그림 10-응용 프로그램 서비스 데이터베이스 역할 추가**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드하는 경우 폼 인증을 사용 하는 방법을 배웠습니다. 첫째, 웹 사이트 관리 도구를 이용 하 여 새 사용자 및 역할을 만드는 방법을 배웠습니다. 다음으로, [Authorize] 특성에서 컨트롤러 작업 호출 권한이 없는 사용자가 방지 하기 위해 사용 하는 방법을 배웠습니다. 마지막으로, 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장 하 여 MVC 응용 프로그램을 구성 하는 방법을 배웠습니다.

>[!div class="step-by-step"]
[이전](preventing-javascript-injection-attacks-cs.md)
[다음](authenticating-users-with-windows-authentication-vb.md)
