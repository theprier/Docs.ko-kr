---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 멤버 자격 | Microsoft Docs
author: microsoft
description: ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다. ASP.NET 폼 인증 incorp 하는 편리한 방법을 제공 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: f776ed628e206c06543589767ba364af3c76ae16
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818219"
---
<a name="membership"></a>멤버 자격
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다. ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 여 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다.


ASP.NET 멤버 자격에서 ASP.NET 폼 인증 모델의 성공을 기반 1.x 합니다. ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 여 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다. FormsAuthentication 클래스의 멤버 수 있도록 인증에 대 한 쿠키를 처리, 유효한 로그인에 대 한 확인, 등으로 사용자를 로그 합니다. 그러나 ASP.NET 1.x 응용 프로그램에서 폼 인증을 구현 하면 많은 양의 코드가 필요할 수 있습니다.

ASP.NET 2.0의 멤버 자격만 폼 인증을 사용 하 여 주요 advancement 경우 (멤버는 폼 인증을 함께 사용 하면 가장 강력한 있지만 폼 인증을 사용 하 여 필요 하지 않습니다.) 곧 보게 되겠지만 사용할 수 있습니다 ASP.NET 멤버 자격 및 로그인 컨트롤 ASP.NET 2.0의 많은 코드를 전혀 작성 하지 않고도 강력한 멤버 자격 시스템을 구현 합니다.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2.0의에서 멤버 자격 구현

멤버 자격 네 단계를 수행 하 여 구현 됩니다. 도 구현할 수 있는 선택적 구성 뿐만 아니라 관련 된 여러 하위 단계는 것을 염두에 두십시오. 멤버 자격을 구성 하는 상황을 큰 그림을 보여 주기 위해 다음이 단계는 것입니다.

1. 멤버 자격 데이터베이스 만들기 (SQL Server 멤버 자격 저장소로 사용 됩니다.) 하는 경우
2. 응용 프로그램 구성 파일에서 멤버 자격 옵션을 지정 합니다. (멤버 자격 기본으로 사용 됩니다.)
3. 사용 하려는 멤버 자격이 저장소 유형을 결정 합니다. 옵션은 같습니다. 

    - Microsoft SQL Server (버전 7.0 이상)
    - Active Directory 저장소
    - 사용자 지정 멤버 자격 공급자
4. ASP.NET 폼 인증을 위해 응용 프로그램을 구성 합니다. 이번에 멤버 자격 폼 인증을 활용 하기 위해 설계 되어 있지만 폼 인증을 사용 하 여 필요 하지 않습니다.
5. 멤버 자격에 대 한 사용자 계정을 정의 하 고 필요한 경우 역할을 구성 합니다.

## <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스를 만드는 중

하는 경우 사용 하 고 SQL Server 7.0을 사용 하 여 aspnet을 나중에 멤버 자격이 저장소로 사용할 수 또는\_regsql 유틸리티 (사용 가능한 가장 쉽게 Visual Studio.NET 2005 명령 프롬프트에서) 데이터베이스를 구성 합니다. Aspnet\_regsql 유틸리티 명령 프롬프트 도구 또는 GUI 마법사를 통해 사용할 수 있습니다. 마법사 방법은 데이터베이스를 구성 하는 가장 쉬운 방법은 합니다. 마법사에 액세스 하려면 다음 명령을 실행 하기만 하면 됩니다.

`aspnet_regsql W`

해당 명령으로 실행 되 면 아래와 같이 ASP.NET SQL Server 설치 마법사를 사용 하 여 표시 수입니다.


![](membership/_static/image1.jpg)

**그림 1**


ASP.NET SQL Server 설치 마법사는 마법사에서 지정한 인스턴스에서 웹 사이트를 만듭니다. 그러나 ASP.NET은 machine.config 파일에 데이터베이스에 연결할 연결 문자열을 사용 합니다. 기본적으로이 연결 문자열은 SQL Server 2005 인스턴스를 가리키게 됩니다 있도록 SQL Server 2000 또는 SQL Server 7.0 인스턴스를 사용 하는 경우 machine.config 파일의 연결 문자열을 수정 해야 합니다. 다음 연결 문자열 찾을 수 있습니다.

[!code-xml[Main](membership/samples/sample1.xml)]

그러나 연결 문자열을 수정 하지 ASP.NET 제공 되지 않습니다 오류를 설명 합니다. 방금 라는 데이터베이스를 만들지 불만을 계속 됩니다. 위의 예에서 내 로컬 SQL Server 2000 인스턴스를 가리키도록 연결 문자열을 수정 했습니다.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>지정 하 여 구성 하 고 추가 사용자 및 역할

멤버 자격 구성의 다음 단계에서는 응용 프로그램의 web.config 파일에 필요한 정보를 추가 하는 것입니다. Asp.net에서 1.x에서 web.config 파일 수정 어려웠습니다 때로는 lowerCamelCase 사용 및 Intellisense의 부족으로 인해. Visual Studio.NET 2005 작업 구성 파일에 Intellisense를 사용 하 여 훨씬 더 쉽게 하지만 ASP.NET 2.0 구성 파일 편집에 대 한 웹 인터페이스를 제공 하 여 한 단계 더 이동 합니다.

솔루션 탐색기 도구 모음 아래와 같이 ASP.NET 구성 단추를 클릭 하 여 웹 인터페이스를 시작할 수 있습니다. 또한 로그인 컨트롤을 삽입할 때 표시 되는 팝업을 통해 웹 인터페이스를 시작할 수 있습니다.


![](membership/_static/image2.jpg)

**그림 2**


그러면 아래에 표시 된 ASP.NET 웹 사이트 관리 도구를 시작 합니다. ASP.NET 웹 사이트 관리에는 손쉽게 응용 프로그램 설정을 관리할 수 있는 4 개의 탭 인터페이스입니다. 다음 탭을 사용할 수 있습니다.

- **Home**
- **보안** 사용자, 역할 및 액세스를 구성 합니다.
- **응용 프로그램** 응용 프로그램 설정을 구성 합니다.
- **공급자** 구성 하 고 응용 프로그램 멤버 자격 공급자를 테스트 합니다.

웹 사이트 관리 도구를 사용 하면 사용자 및 역할 관리를 간편 하 게 새 사용자 만들기, 새 역할을 만들 수 있습니다. 이 기능은 사용할 수 없는 경우 Windows 인터페이스에서 Windows 인터페이스를 사용 하면 권한 부여 설정을 쉽게 정의할 수 및 추가, 삭제 및 공급자, 웹 사이트 관리 도구에 없는 기능을 관리할 수 있습니다.

Windows 인터페이스를 시작 하려면 인터넷 정보 서비스 스냅인을 열고 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다. 속성을 선택 합니다. ASP.NET 탭을 클릭 하 고 구성 편집 단추를 클릭 합니다. (응용 프로그램을 사용할 구성 편집 단추에 대 한 ASP.NET 2.0에서 실행 되어야 합니다. 물론 ASP.NET 대화 상자에서 ASP.NET 버전을 구성할 수 있습니다) ASP.NET 구성 설정 대화 상자는 아래와 같이 표시 됩니다.


![](membership/_static/image3.jpg)

**그림 3**


일반 탭의 연결 문자열 및 응용 프로그램 설정을 나열 됩니다. 기울임꼴로 표시 설정을 상위 구성 파일 (machine.config 또는 높은 수준에서 web.config)에 정의 된 및 기울임꼴에 없는 설정은 응용 프로그램 구성 파일에서 합니다. 설정이 추가 된 경우 제거 되거나 응용 프로그램 수준에서 편집 ASP.NET은 추가, 제거 또는 상속 된 구성 파일에서 설정을 제거 하는 대신 응용 프로그램 수준 web.config에서 설정을 수정 합니다.

인증 탭은 다음과 같습니다. 이 멤버 자격 설정을 구성 합니다. 인증 설정, 멤버 자격 공급자를 구성 하 고 역할 공급자를 여기서 구성할 수 있습니다.


![](membership/_static/image4.jpg)

**그림 4**


## <a name="implementing-membership-in-your-application"></a>멤버 자격 응용 프로그램에서 구현

응용 프로그램에서 ASP.NET 2.0 멤버 자격을 구현 하는 가장 쉬운 방법은 제공 된 로그온 컨트롤을 사용 하는 것입니다. 이 메서드를 사용 하면 모든 코드를 전혀 작성 하지 않고도 ASP.NET 2.0 멤버 자격의 기본 사항을 구현할 수 있습니다.

다음 로그온 컨트롤은 ASP.NET 2.0에서 사용할 수 있습니다.

## <a name="login-control"></a>로그인 컨트롤

Login 컨트롤 멤버 자격 시스템에 로그인 할 사용자 인터페이스를 제공 합니다. 사용자 이름 및 암호 textboxt 및 로그인 단추를 사용 하 여 제공 합니다. 권한이 있는 사용자에 대 한 등록에 대 한 링크와 같은 기타 일반적인 여러 기능 수행 되므로 확인란을 허용 하는 자동으로 로그인 하면 후속 아직 방문 등 암호 힌트에 대 한 링크입니다. Login 컨트롤의 모든 기능을 컨트롤의 속성을 통해 사용자 지정할 수 있습니다.

Asp.net에서 1.x에서 개발자는 상당한 양의 폼 인증을 사용 하는 경우 조회를 수행 하는 코드를 작성 해야 했습니다. ASP.NET 2.0 멤버 자격을 사용 하 여 코드를 전혀 작성 하지 않고 사용자를 확인할 수 있습니다. ASP.NET는 수에 자동으로 사용자의 조회를 수행 합니다. (ASP.NET 멤버 자격을 사용 하지 않고 로그인 컨트롤을 사용 중인 경우 사용할 수 있습니다 합니다 **OnAuthenticate** 사용자의 유효성을 검사 하는 방법입니다.)

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤은 기본적으로 두 개의 템플릿이 제공 하는 템플릿 기반 컨트롤 AnonymousTemplate 및 LoggedInTemplate 합니다. 표시 되는 템플릿은 사용자가 멤버 자격 시스템에 로그인 여부 의해 결정 됩니다. 이 컨트롤은 사용자가 로그인 하는 경우 사용자가 아직 로그인 하지 않은 경우 로그인 컨트롤 및 LoginStatus 컨트롤 및/또는 다른 로그인 컨트롤을 표시 하려면 일반적으로 사용 됩니다. 역할 관리를 ASP.NET 응용 프로그램에서 사용 하는 경우 사용자 역할에 따라 특정 템플릿을 LoginView 컨트롤에 표시할 수 있습니다. (더 asp.net 역할 관리 다룰 나중.)

## <a name="passwordrecovery-control"></a>PasswordRecovery 컨트롤

PasswordRecovery 컨트롤을 사용 하면 자신의 현재 암호를 사용 하 여 전자 메일을 받거나 자신의 암호를 재설정할 수 있습니다. 일반 텍스트 및 암호화 된 암호 복구 하 고 사용자에 게 메일로 전송 될 수 있습니다. 해시 된 암호는 복구할 수 없습니다. 대신 사용자 암호 재설정을 수행 해야 합니다.

## <a name="loginstatus-control"></a>LoginStatus 컨트롤

LoginStatus 컨트롤에는 현재 로그인 한 사용자에 게 로그인 하지 않은 사용자는 로그인 표시기 및 로그 아웃 표시기 표시 됩니다. Request.IsAuthenticated 속성을 표시 하는 표시기를 확인 하려면 사용 됩니다. LoginStatus 컨트롤에서 표시 하는 표시기 텍스트일 수 있습니다 (를 통해 구현 된 **LoginText** 및 **LogoutText** 속성) 또는 이미지 (통해 구현를 **LoginImageUrl**하 고 **LogoutImageUrl** 속성입니다.)

자신이 지정 된 URL로 리디렉션되면 사용자가 LoginStatus 컨트롤을 통해 로그 아웃할 때 합니다 **LogoutPageUrl** 속성입니다. 해당 속성을 설정 하지 않으면 하는 경우 현재 페이지 새로 고쳐집니다. 사이트는 Forms 인증으로 보호 가능성이 있으므로 현재 페이지의 새로 고침이 사이트에 대 한 로그인 페이지로 사용자를 리디렉션합니다.

## <a name="loginname-control"></a>LoginName 컨트롤

LoginName 컨트롤 사이트에 현재 로그인 한 사용자의 사용자를 표시 합니다.

## <a name="createuserwizard-control"></a>CreateUserWizard 컨트롤

CreateUserWizard 컨트롤은 멤버 자격 시스템에 등록 하는 편리한 방법을 제공 합니다. 아래에 표시 된 인터페이스를 통해 (WizardSteps 컬렉션으로 구현 됨) 하는 단계를 추가할 수 있습니다.


![](membership/_static/image5.jpg)

**그림 5**


CreateUserWizard는 마법사 클래스에서 파생 되 고 다음 템플릿을 제공 하는 템플릿 기반 컨트롤은 같습니다.

- **머리글 템플릿의** 이 템플릿 마법사의 헤더의 모양을 제어 합니다.
- **SidebarTemplate** 이 템플릿 마법사의 세로 막대의 모양을 제어 합니다.
- **StartNavigationTemplate** 탐색의 모양을 시작 단계에서 마법사는이 템플릿 제어 합니다.
- **StepNavigationTemplate** 이 템플릿은 시작 또는 완료 단계에 없는 경우 탐색 영역의 모양을 제어 합니다.
- **FinishNavigationTemplate** 이 서식 파일 마침 단계에서 작업 하는 경우 탐색 영역의 모양을 제어 합니다.

또한 마법사에 추가한 각 단계에서는 ASP.NET을 ContentTemplate 및 해당 단계에 대 한 CustomNavigationTemplate 모두 포함 하는 사용자 지정 템플릿을 만들어집니다. CreateUserWizard 사용자 지정에 대 한 전체 내용은 VS.NET 2005 설명서를 참조 하십시오.

## <a name="changepassword-control"></a>ChangePassword 컨트롤

ChangePassword 컨트롤에는 사용자를 자신의 암호를 변경할 수 있습니다. DisplayUserName 속성 (기본적으로 false 임) true 인 경우에 기록 되지 않습니다 하는 경우 사용자가 자신의 암호를 변경할 수입니다. 하는 경우 사용자 *는* 이미 로그인 DisplayUserName 속성이 true를 사용자가 해당 사용자의 사용자 ID를 알고 있는 제공 로그인 하지 않은 다른 사용자의 암호를 변경 하는 일을 할 수 있습니다.

사용자가 로그인 하지 않고도 암호를 변경할 수 있도록 원한다 면 해야 ChangePassword 컨트롤 표시 되는 페이지 익명 액세스를 허용 하는지 확인 염두에 두어야 합니다. 물론 사용자가 자신의 암호를 변경 하기 위해 이전 암호를 제공 해야 합니다.

## <a name="role-management"></a>역할 관리

역할 관리를 사용 하면 특정 역할에 사용자를 할당 하 고 한 특정 파일 또는 폴더는 역할 기반 액세스를 제한할 수 있습니다. 역할 관리는 또한 프로그래밍 방식으로 someones 역할 확인 또는 특정 역할에는 모든 사용자를 적절 하 게 대응할 수 있도록 API를 제공 합니다.

역할 관리 ASP.NET 멤버 자격에 필요 하지 않은 멤버 자격 역할 관리를 사용 하려면 요구 사항입니다. 그러나 두 원활 하 게 서로 보완 하며는 개발자는 함께 사용할 서로 가능성이 높습니다.

응용 프로그램에서 역할 관리를 사용 하려면 web.config 파일에 다음 변경 내용을 확인 합니다.

[!code-xml[Main](membership/samples/sample2.xml)]

경우는 **cacheRolesInCookie** 특성이로 설정 된 물론 ASP.NET 캐시 클라이언트의 쿠키에 사용자 역할 멤버 자격. 이 역할 공급자를 호출 하지 않고 역할 조회 수 있습니다. 개발자는 되도록 하려면이 특성을 사용 하는 경우는 **cookieProtection** 특성 All로 설정 됩니다. (기본 설정입니다.) 이렇게 하면 쿠키 데이터를 암호화 된 쿠키 내용을 변경 하지 않도록 하는 데 도움이 됩니다. 웹 사이트 관리 도구를 사용 하 여 역할을 추가할 수 있습니다. 쉽게 역할 정의 해당 역할에 기반 하 여 사이트의 부분에 대 한 액세스를 구성 하 고 역할에 사용자를 할당할 수 있습니다.


![](membership/_static/image6.jpg)

**그림 6**


위와 같이 역할의 이름을 입력 하는 것 다음 역할 추가 클릭 하 여 새 역할을 추가할 수 있습니다. 기존 역할을 관리 하거나 기존 역할 목록에서 적절 한 링크를 클릭 하 여 삭제할 수 있습니다.

역할을 관리 하는 경우에 추가 하거나 아래와 같이 사용자를 제거할 수 있습니다.


![](membership/_static/image7.jpg)

**그림 7**


확인란 역할에 사용자를 특정 역할에 사용자를 쉽게 추가할 수 있습니다. ASP.NET에 적절 한 항목을 사용 하 여 멤버 자격 데이터베이스를 자동으로 업데이트 됩니다. 응용 프로그램에 대 한 액세스 규칙을 구성 하려고도 합니다. ASP.NET 1.x 개발자가이 통해 작업을 수행 합니다 &lt;권한 부여&gt; web.config 파일에서 해당 옵션에는 요소는 ASP.NET 2.0에서 계속 사용할 수 있습니다. 그러나 것 액세스를 관리 하는 것이 더 쉬워졌습니다 규칙은 웹 사이트 관리 도구 표시 된 것 처럼 다음을 사용 하 여 합니다.


![](membership/_static/image8.jpg)

**그림 8**


이 경우 관리 폴더 강조 표시 됩니다 (해당 고급 도구 밝은 회색으로 강조 표시 되므로 보려는) 및 관리자 역할에 액세스할 수 합니다. 다른 모든 사용자는 거부 됩니다. 규칙을 선택한 다음 위로 및 아래로 이동 단추를 사용 하 여 규칙을 정렬 하려면 헤드 아이콘을 클릭할 수 있습니다. ASP.NET과 마찬가지로 &lt;권한 부여&gt; 요소 규칙은 나타나는 순서 대로 처리 됩니다. 즉, 위의 샷에 규칙의 순서 반전 된 경우 되므로 ASP.NET 발생 하 게 하는 첫 번째 규칙 폴더에 모든 사용자를 거부 하는 규칙 관리 폴더에 액세스할을 수는 없습니다.

ASP.NET 2.0는 액세스 규칙을 지정 하는 폴더에 web.config 파일을 추가 합니다. 구성 파일 또는 웹 사이트 관리 도구를 통해 액세스 규칙을 편집할 수 있습니다. 즉, 웹 사이트 관리 도구는 인터페이스는 구성 파일 친숙 한 환경에서 편집할 수 있습니다.

## <a name="using-roles-in-code"></a>코드에서 역할 사용

역할 관리에 대 한 API 버전 이후 변경 되지 않은 1.x 합니다. **IsInRole** 메서드는 하는 데 사용자가 특정 역할에 있는지 확인 합니다.

[!code-csharp[Main](membership/samples/sample3.cs)]

또한 ASP.NET 현재 컨텍스트의 멤버로 파트너가 인스턴스를 만듭니다. 파트너가 개체는 사용자가 속한 역할을 다음과 같이 모든를 가져오는 데 사용할 수 있습니다.

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>RoleGroups LoginView 컨트롤 사용

멤버 자격 및 역할 관리 이해 했으므로 통해 LoginView 컨트롤은 ASP.NET 2.0에서이 기능을 사용 하는 방법을 간략하게 설명 있습니다. 앞에서 설명한 대로 LoginView 컨트롤은 기본적으로 두 개의 템플릿이 포함 된 템플릿 기반 컨트롤 AnonymousTemplate 및 LoggedInTemplate 합니다. 내 LoginView 대화 상자는 아래와 같이 링크는 작업 RoleGroups 편집할 수 있습니다.


![](membership/_static/image9.jpg)

**그림 9**


각 RoleGroup 개체 RoleGroup 적용 되는 역할을 정의 하는 문자열의 배열을 포함 합니다. 새 RoleGroup LoginView 컨트롤에 추가 하려면 RoleGroups 편집 링크를 클릭 합니다. 위의 이미지에서 추가한 것 관리자에 대 한 새 RoleGroup 볼 수 있습니다. 해당 RoleGroup를 선택 하 여 (RoleGroup[0]) 뷰 드롭다운 목록에서 있습니까 템플릿을 구성할 수만 관리자 역할의 멤버에 게 표시 되는 합니다. 아래 이미지에서는 Sales 역할 및 배포 역할의 멤버에 적용 되는 새 RoleGroup 추가 했습니다. 두 번째 RoleGroup LoginView 작업 대화 상자에서 뷰 드롭다운 목록에 추가 하 고 해당 템플릿을 추가할 모든 판매 또는 배포의 모든 사용자가 볼 수 있습니다 역할입니다.


![](membership/_static/image10.jpg)

**그림 10**


## <a name="overriding-the-existing-membership-provider"></a>기존 멤버 자격 공급자를 재정의합니다.

ASP.NET 멤버 자격의 기능을 확장 하는 방법의 몇 가지 있습니다. 먼저,에서 상속 하 고 해당 메서드를 재정의 하 여 SqlMembershipProvider 클래스의 기존 기능을 확실히 변경할 수 있습니다. 예를 들어, 사용자를 만들 때 고유한 기능을 구현 하려는 경우에 다음과 같이 SqlMembershipProvider에서 상속 되는 고유한 클래스를 만들 수 있습니다.

[!code-csharp[Main](membership/samples/sample5.cs)]

공급자 (예를 들어 Access 데이터베이스에 멤버 자격 정보를 저장)를 직접 만들려면 하려는 다른 한편으로, 경우에 고유한 공급자를 만들 수 있습니다.

## <a name="creating-your-own-membership-provider"></a>직접 멤버 자격 공급자 만들기

직접 멤버 자격 공급자를 만들려면 먼저 해야 MembershipProvider 클래스에서 상속 되는 클래스를 만듭니다. VB.NET를 사용 하는 경우 Visual Studio 2005는 모든 메서드를 재정의 해야 하는 한 스텁이 자동으로 추가 합니다. C#에서는 해당 최대 스텁이 추가할 수 있습니다 사용 중인 경우.

다음 재정의 해야 합니다.

- ApplicationName 속성
- ChangePassword 함수
- ChangePasswordQuestionAndAnswer 함수
- CreateUser 함수
- DeleteUser 함수
- EnablePasswordReset 속성
- EnablePasswordRetrieval 속성
- FindUsersByEmail 함수
- FindUsersByName 함수
- GetAllUsers 함수
- GetNumberOfUsersOnline 함수
- GetPassword 함수
- GetUser 함수
- GetUserNameByEmail 함수
- MaxInvalidPasswordAttempts 속성
- MinRequiredNonAlphanumericCharacters 속성
- MinRequiredPasswordLength 속성
- PasswordAttemptWindow 속성
- PasswordFormat 속성
- PasswordStrengthRegularExpression 속성
- RequiresQuestionAndAnswer 속성이
- RequiresUniqueEmail 속성
- ResetPassword 함수
- 사용자 함수를 잠금 해제
- 하기 위한 함수
- ValidateUser 함수

Thats C# 개발자로 서 구현 목록입니다. Vb.net에서 구현을 제외한 클래스를 만들고 다음 C# 코드를 변환할.NET Reflector 또는 유사한 도구를 사용 하는 작업을 쉽게 찾을 수 있습니다.

연결 문자열 및 기타 속성을 기본값으로 초기화 메서드에서 설정 되어야 합니다. (Initialize 메서드는 발생 공급자가 런타임에 로드 합니다.) Initialize 메서드의 두 번째 매개 변수 형식이 System.Collections.Specialized.NameValueCollection 며에 대 한 참조를 &lt;추가&gt; web.config 파일에서 사용자 지정 공급자와 연결 된 요소입니다. 해당 항목은 다음과 같습니다.

[!code-xml[Main](membership/samples/sample6.xml)]

Initialize 메서드의 예로 다음과 같습니다.

[!code-csharp[Main](membership/samples/sample7.cs)]

사용자의 로그인 양식을 제출할 때 유효성을 검사 하기 위해 ValidateUser 메서드를 사용 해야 합니다. 이 메서드는 사용자 로그인 컨트롤의 로그인 단추를 클릭할 때 발생 합니다. 이 메서드에서 사용자 조회를 수행 하는 코드를 배치 됩니다.

알 수 있듯이 직접 멤버 자격 공급자를 작성은 어렵지 않습니다 하 고 ASP.NET 2.0의이 강력한 기능을 확장할 수 있습니다.
