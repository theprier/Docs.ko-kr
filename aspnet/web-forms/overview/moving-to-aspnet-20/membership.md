---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: "멤버 자격 | Microsoft Docs"
author: microsoft
description: "ASP.NET에서 폼 인증 모델의 성공 여부에 ASP.NET 멤버 자격을 빌드합니다 1.x 합니다. ASP.NET 폼 인증 incorp 하는 편리한 방법을 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: 1a5a495845b60f9aac51c9776311af67f5dc8767
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="membership"></a>멤버 자격
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET에서 폼 인증 모델의 성공 여부에 ASP.NET 멤버 자격을 빌드합니다 1.x 합니다. ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 고 사용자는 데이터베이스 또는 다른 데이터 저장소에 대해 유효성을 검사 하는 편리한 방법을 제공 합니다.


ASP.NET에서 폼 인증 모델의 성공 여부에 ASP.NET 멤버 자격을 빌드합니다 1.x 합니다. ASP.NET 폼 인증에는 ASP.NET 응용 프로그램에 로그인 폼을 통합 하 고 사용자는 데이터베이스 또는 다른 데이터 저장소에 대해 유효성을 검사 하는 편리한 방법을 제공 합니다. FormsAuthentication 클래스의 멤버는 인증용 쿠키를 처리, 유효한 로그인에 대 한 확인, 사용자 등 아웃 수 있도록 설정 합니다. 그러나 ASP.NET 1.x 응용 프로그램에서 폼 인증을 구현 하면 많은 양의 코드가 필요할 수 있습니다.

ASP.NET 2.0의 구성원만 폼 인증을 사용 하 여 위에 비교해 크게입니다. (멤버 자격은 폼 인증을 함께 사용 하면 가장 강력한 있지만 폼 인증을 사용 하 여 필요 하지 않습니다.) 곧 알게 사용할 수 있습니다 ASP.NET 멤버 자격 및 로그인 컨트롤 ASP.NET 2.0에서 많은 코드를 전혀 작성 하지 않고도 강력한 멤버 자격 시스템을 구현 하려면.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2.0에서에서 멤버 자격을 구현합니다.

4 단계에 따라 멤버 자격 구현 됩니다. 도 구현할 수 있는 선택적 구성 뿐만 아니라 관련 된 여러 하위 단계는 염두에서에 둬야 합니다. 멤버 자격을 구성 하는의 큰 그림을 설명 하기 위해 이러한 단계는 것입니다.

1. 멤버 자격 데이터베이스 만들기 (SQL Server 멤버 자격이 저장소로 사용 됩니다.) 하는 경우
2. 응용 프로그램 구성 파일의 멤버 자격 옵션을 지정 합니다. (멤버 자격 기본적으로 사용 됩니다.)
3. 사용 하려는 멤버 자격 저장소의 유형을 결정 합니다. 옵션은 같습니다. 

    - Microsoft SQL Server (버전 7.0 이상)
    - Active Directory 저장소
    - 사용자 지정 멤버 자격 공급자
4. ASP.NET 폼 인증에 대 한 응용 프로그램을 구성 합니다. 다시 한 번 멤버는 폼 인증을 활용 하도록 만들어졌지만 폼 인증을 사용 하 여 필요 하지 않습니다.
5. 멤버 자격에 대 한 사용자 계정을 정의 하 고 원하는 경우 역할을 구성 합니다.

## <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스 만들기

하는 경우 사용 하 고 SQL Server 7.0을 사용 하 여 aspnet 나중에 멤버 자격이 저장소로 사용할 수 있습니다 또는\_regsql 유틸리티 (사용 가능한 가장 쉽게에서 Visual Studio.NET 2005 명령 프롬프트) 데이터베이스를 구성 해야 합니다. Aspnet\_regsql 유틸리티 명령 프롬프트 도구 또는 GUI 마법사를 통해 사용할 수 있습니다. 마법사 방법은 가장 쉬운 방법은 데이터베이스를 구성 해야 합니다. 마법사에 액세스 하려면 다음 명령을 실행 하면 됩니다.

`aspnet_regsql W`

해당 명령을 실행 하면 일단 나타납니다 ASP.NET SQL Server 설치 마법사를 다음과 같이 합니다.


![](membership/_static/image1.jpg)

**그림 1**


ASP.NET SQL Server 설치 마법사는 마법사에서 지정한 인스턴스에서 웹 사이트를 만듭니다. 그러나 ASP.NET 사용자 데이터베이스에 연결 하는 machine.config 파일에 연결 문자열을 사용 합니다. 기본적으로이 연결 문자열은 SQL Server 2005 인스턴스를 가리킬 때문 SQL Server 2000 또는 SQL Server 7.0 인스턴스를 사용 하는 경우 machine.config 파일의 연결 문자열을 수정 해야 합니다. 연결 문자열을 여기 찾을 수 있습니다.

[!code-xml[Main](membership/samples/sample1.xml)]

그러나 연결 문자열을 수정 하지 않는 경우 ASP.NET 제공 되지 않습니다 설명 하는 오류입니다. 방금 라는 데이터베이스를 만들지 않은 불만을 계속 됩니다. 위의 경우에 내 로컬 SQL Server 2000 인스턴스를 가리키도록 연결 문자열을 수정 했습니다 I.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>구성 추가 사용자 및 역할 지정

멤버 자격을 구성 하는 다음 단계는 응용 프로그램의 web.config 파일에 필요한 정보를 추가 하는 것입니다. ASP.NET에서 web.config 파일 수정 1.x가 어려웠습니다 경우에 따라 intellisense와 lowerCamelCase 사용으로 인해. ASP.NET 2.0 구성 파일 편집에 대 한 웹 인터페이스를 제공 하 여 한 단계 더 발전 라인 낮지만 visual Studio.NET 2005 작업 구성 파일에 Intellisense 사용 하 여 훨씬 더 쉽게 만듭니다.

솔루션 탐색기 도구 모음 아래와 같이 ASP.NET 구성 단추를 클릭 하 여 웹 인터페이스를 시작할 수 있습니다. Login 컨트롤 삽입 되는 경우 표시 되는 팝업을 통해 웹 인터페이스를 시작할 수 있습니다.


![](membership/_static/image2.jpg)

**그림 2**


아래에 표시 된 ASP.NET 웹 사이트 관리 도구를 시작 합니다. ASP.NET 웹 사이트 관리는 응용 프로그램 설정 관리를 활용할 수 있는 4 개의 탭 인터페이스입니다. 다음과 같은 탭을 사용할 수 있습니다.

- **홈**
- **보안** 사용자, 역할 및 액세스를 구성 합니다.
- **응용 프로그램** 응용 프로그램 설정을 구성 합니다.
- **공급자** 구성 및 응용 프로그램 멤버 자격 공급자를 테스트 합니다.

웹 사이트 관리 도구를 사용 하 여 사용자 및 역할 관리를 쉽게 새 사용자를 만들고, 새 역할을 만들 수 있습니다. 이 기능은 사용할 수 없는 경우 Windows 인터페이스의 Windows 인터페이스를 사용 하면 권한 부여 설정을 쉽게 정의할 추가, 삭제 및 공급자, 웹 사이트 관리 도구에 없는 기능을 관리할 수 있습니다.

Windows 인터페이스를 시작 하려면 인터넷 정보 서비스 스냅인을 사용 하 여 열고 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다. 속성을 선택 합니다. ASP.NET 탭을 클릭 하 고 구성 편집 단추를 클릭 합니다. (응용 프로그램을 사용할 구성 편집 단추에 대 한 ASP.NET 2.0에서 실행 되어야 합니다. ASP.NET 대화 상자에 ASP.NET 버전을 구성할 수 있습니다) ASP.NET 구성 설정 대화 상자는 아래와 같이 표시 됩니다.


![](membership/_static/image3.jpg)

**그림 3**


일반 탭에서 연결 문자열 및 응용 프로그램 설정을 나열 됩니다. 기울임꼴로 표시에 없는 설정은 응용 프로그램 구성 파일에서 및 기울임꼴로 설정을 부모 구성 파일 (machine.config 또는 더 높은 수준에서 web.config)에 정의 됩니다. 설정이 추가 된 경우 제거 됨 또는 응용 프로그램 수준에서 편집할 ASP.NET 됩니다 추가, 제거 또는 상속 된 구성 파일에서 해당 설정을 제거 하는 대신 응용 프로그램 수준 web.config에서 설정을 수정 합니다.

인증 탭은 아래와 같습니다. 이 멤버 자격 설정을 구성 합니다. 멤버 자격 공급자 인증 설정 구성 및 역할 공급자는 여기에 구성할 수 있습니다.


![](membership/_static/image4.jpg)

**그림 4**


## <a name="implementing-membership-in-your-application"></a>멤버 자격 응용 프로그램에서 구현

응용 프로그램에서 ASP.NET 2.0 멤버 자격을 구현 하는 가장 쉬운 방법은 제공 된 로그온 컨트롤을 사용 하는 것입니다. 이 메서드를 사용 하면 코드를 전혀 작성 하지 않고 ASP.NET 2.0 멤버 자격의 기본 사항을 구현할 수 있습니다.

다음 로그온 컨트롤은 ASP.NET 2.0에서 사용할 수 있습니다.

## <a name="login-control"></a>Login 컨트롤

Login 컨트롤 멤버 자격 시스템에 로그인 할 다른 사용자에 대 한 인터페이스를 제공 합니다. 사용자 이름 및 암호 textboxt 및 로그인 단추가 제공합니다. 다른 공통적인 기능이 많이 후속 방문 시 자동으로 로그인에 사용자를 허용 하는 확인란을 선택 하므로 아직 수행 하지 않은 사용자를 위해 등록에 대 한 링크, 암호 미리 알림을 등에 대 한 링크입니다. Login 컨트롤의 모든 기능을 컨트롤의 속성을 통해 사용자 지정할 수 있습니다.

ASP.NET에서 1.x 개발자가 한 상당한 양의 폼 인증을 사용 하는 경우에 조회를 수행 하는 코드를 작성 해야 했습니다. ASP.NET 2.0 멤버 코드를 전혀 작성 하지 않고 사용자가 확인할 수 있습니다. 자동으로 ASP.NET 사용자에 대 한 사용자의 조회를 수행 합니다. (ASP.NET 멤버 자격을 사용 하지 않고 로그인 제어를 사용 하는 경우 사용할 수 있습니다는 **OnAuthenticate** 메서드를 사용자의 유효성을 검사 합니다.)

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤은 기본적으로 두 개의 템플릿이 제공 하는 템플릿 기반 컨트롤 AnonymousTemplate 및는 LoggedInTemplate 합니다. 표시 되는 서식 파일은 멤버 자격 시스템에 사용자가 로그인 하는 여부 의해 결정 됩니다. 이 컨트롤은 사용자가 로그인 하는 경우 사용자가 아직 로그인 하지 않은 경우 Login 컨트롤 및 LoginStatus 컨트롤 및/또는 다른 로그인 컨트롤을 표시 하려면 일반적으로 사용 됩니다. 역할 관리 ASP.NET 응용 프로그램을 사용 하는 경우 사용자 역할에 따라 특정 템플릿을 LoginView 컨트롤에 표시할 수 있습니다. (더 asp.net 역할 관리가 살펴보겠습니다 나중.)

## <a name="passwordrecovery-control"></a>PasswordRecovery 제어

PasswordRecovery 컨트롤에는 사용자를 자신의 현재 암호를 사용 하는 메일이 또는 암호를 다시 설정할 수 있습니다. 일반 텍스트와 암호화 된 암호 복구 및 사용자에 게 메일로 보낼 수 있습니다. 암호가 해시 되는지 복구할 수 없습니다. 대신 사용자는 암호 재설정을 수행 해야 합니다.

## <a name="loginstatus-control"></a>LoginStatus 제어

LoginStatus 컨트롤을 사용 하 여 현재 로그인에 사용자에 게 로그인 하지 않은 사용자에 게 로그인 표시기 및 로그 아웃 표시기를 표시 합니다. Request.IsAuthenticated 속성은 표시 하지는 않으려면 확인 하려면 사용 합니다. LoginStatus 컨트롤에서 표시 하는 표시기 텍스트일 수 있습니다 (통해 구현는 **LoginText** 및 **LogoutText** 속성) 또는 이미지 (을 통해 구현 되는 **LoginImageUrl**및 **LogoutImageUrl** 속성입니다.)

자신이 하 여 지정 된 URL로 리디렉션되면 LoginStatus 컨트롤을 통해 사용자 로그 아웃 하는 경우는 **LogoutPageUrl** 속성입니다. 해당 속성을 설정 하지 않으면 현재 페이지가 새로 고쳐집니다. 사이트는 폼 인증으로 보호 되어 가능성이, 있으므로 현재 페이지의 새로 고침은 사용자를 사이트에 대 한 로그인 페이지로 리디렉션합니다.

## <a name="loginname-control"></a>LoginName 컨트롤

LoginName 컨트롤 사이트에 현재 로그인 한 사용자의 사용자를 표시 합니다.

## <a name="createuserwizard-control"></a>CreateUserWizard 컨트롤

CreateUserWizard 컨트롤은 멤버 자격 시스템을 등록 하는 편리한 방법을 제공 합니다. 아래에 표시 된 인터페이스를 통해 (WizardSteps 컬렉션으로 구현 됨) 하는 단계를 추가할 수 있습니다.


![](membership/_static/image5.jpg)

**그림 5**


CreateUserWizard 마법사 클래스에서 파생 되 고 다음 템플릿을 제공 하는 템플릿 기반 컨트롤은입니다.

- **HeaderTemplate** 이 템플릿 마법사의 헤더의 모양을 제어 합니다.
- **SidebarTemplate** 이 서식 파일은 마법사의 세로 막대의 모양을 제어 합니다.
- **StartNavigationTemplate** 탐색의 모양을 시작 단계에서 마법사는이 템플릿 제어 합니다.
- **StepNavigationTemplate** 이 서식 파일 중이 아닌 경우 시작 또는 완료 단계 탐색 영역의 모양을 제어 합니다.
- **FinishNavigationTemplate** 이 서식 파일 마침 단계에서 작업 하는 경우 탐색 영역의 모양을 제어 합니다.

또한 마법사에 추가 하는 각 단계에서는 ASP.NET는 ContentTemplate와 해당 단계에 대 한 CustomNavigationTemplate 모두 포함 하는 사용자 지정 템플릿을 만들어집니다. CreateUserWizard 사용자 지정에 자세한 내용은 VS.NET 2005 설명서를 참조 합니다.

## <a name="changepassword-control"></a>ChangePassword 제어

ChangePassword 컨트롤에는 사용자를 자신의 암호를 변경할 수 있습니다. DisplayUserName 속성이 (기본적으로 false는) true 이면 사용자에 기록 되지 않습니다 때 암호를 변경할 수 있습니다. 하는 경우 사용자 *은* 이미 로그인 및 DisplayUserName 속성이 true 이면 사용자가 해당 사용자의 사용자 ID를 알고 제공 로그인 하지 않은 다른 사용자의 암호를 변경할 수 있습니다.

사용자가 로그인 할 필요 없이 암호를 변경할 수 있도록 하려는 ChangePassword 컨트롤이 표시 되는 페이지에 익명 액세스를 허용 하는지 확인 해야 합니다는 염두에서에 둬야 합니다. 물론, 사용자가 암호를 변경 하기 위해 이전 암호를 제공 해야 합니다.

## <a name="role-management"></a>역할 관리

역할 관리를 사용 하면 특정 역할에 사용자를 할당 하 고 다음 특정 파일 또는 폴더를 해당 역할에 따라 액세스를 제한할 수 있습니다. 역할 관리는 또한 프로그래밍 방식으로 someones 역할을 확인 또는 특정 역할에는 모든 사용자를 확인할 수 있고 적절 하 게 응답 있도록 API를 제공 합니다.

역할 관리는 ASP.NET 멤버 자격에 대 한 요구 사항이 아닙니다 하거나 멤버 자격 역할 관리를 사용 하려면 요구 사항입니다. 그러나 두 원활 하 게 서로 보완 하며 사용할 수 있다는 점 개발자는 서로 함께 높습니다.

응용 프로그램에서 역할 관리를 사용 하려면 다음과 같이 변경 web.config 파일에:

[!code-xml[Main](membership/samples/sample2.xml)]

경우는 **cacheRolesInCookie** 특성이로 설정 된 true 이면 ASP.NET 캐시 클라이언트의 쿠키에 사용자 역할 구성원 자격. 따라서 역할 조회를 RoleProvider 호출 하지 않고 발생할 수 있습니다. 개발자는 되도록 하려면이 특성을 사용 하는 경우는 **cookieProtection** 특성을 All로 설정 됩니다. (이것이 기본 설정입니다.) 이렇게 하면 쿠키 데이터가 암호화 된 쿠키 내용을 변경 하지 않도록 하는 데 도움이 됩니다. 웹 사이트 관리 도구를 사용 하 여 역할을 추가할 수 있습니다. 쉽게 역할 정의 해당 역할에 따라 사이트의 부분에 대 한 액세스를 구성 하 고 사용자 역할에 할당할 수 있습니다.


![](membership/_static/image6.jpg)

**그림 6**


위와 같이 단순히 역할의 이름을 입력 하 고 역할 추가 클릭 하 여 새 역할을 추가할 수 있습니다. 기존 역할을 관리 하거나 기존 역할의 목록에서 적절 한 링크를 클릭 하 여 삭제할 수 있습니다.

역할을 관리 하는 경우에 추가 하거나 아래와 같이 사용자를 제거할 수 있습니다.


![](membership/_static/image7.jpg)

**그림 7**


역할에 사용자 확인란을 선택 하 여 특정 역할에 사용자를 쉽게 추가할 수 있습니다. ASP.NET의 해당 항목이 멤버 자격 데이터베이스를 자동으로 업데이트 됩니다. 또한 응용 프로그램에 대 한 액세스 규칙을 구성 합니다. ASP.NET 1.x 개발자가이 통해 수행 하는 &lt;권한 부여&gt; web.config 파일 및 해당 옵션에는 요소는 ASP.NET 2.0에서 계속 제공 합니다. 그러나 액세스를 관리 하는 보다 쉽게 규칙은 웹 사이트 관리 도구와 같이 아래를 사용 하 여 합니다.


![](membership/_static/image8.jpg)

**그림 8**


이 경우 관리 폴더 강조 표시 됩니다 (해당 보기 어려울 도구 밝은 회색으로 강조 표시 하기 때문에) 및 관리자 역할에 대 한 액세스 부여 합니다. 다른 모든 사용자가 거부 됩니다. 규칙을 선택한 다음 위로 이동 및 아래로 이동 단추를 사용 하 여 규칙을 정렬 하려면 헤드 아이콘을 클릭할 수 있습니다. ASP.NET과 마찬가지로 &lt;권한 부여&gt; 요소 규칙은 나타나는 순서 대로 처리 됩니다. 즉, 위에 나와 있는 규칙의 순서 순서가 바뀐 경우 아무도 것 액세스 관리 폴더 있기 때문에 첫 번째 규칙 ASP.NET 발생 하는 것을 폴더에 모든 사용자를 거부 하는 규칙입니다.

ASP.NET 2.0 액세스 규칙을 지정 하는 폴더에 web.config 파일을 추가 합니다. 구성 파일 또는 웹 사이트 관리 도구를 통해 액세스 규칙을 편집할 수 있습니다. 즉, 웹 사이트 관리 도구는 인터페이스는 구성 파일 친숙 한 환경에서 편집할 수 있습니다.

## <a name="using-roles-in-code"></a>코드에서 역할을 사용 하 여

역할 관리에 대 한 API 버전 이후 변경 되지 않은 1.x 합니다. **IsInRole** 메서드는 특정 역할에는 사용자가 인지 확인 하는 데 사용 됩니다.

[!code-csharp[Main](membership/samples/sample3.cs)]

또한 ASP.NET 현재 컨텍스트의 멤버로 RolePrincipal 인스턴스를 만듭니다. RolePrincipal 개체는 사용자가 속한 역할을 다음과 같이 모든를 가져오는 데 사용할 수 있습니다.

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>LoginView 컨트롤 RoleGroups 사용

이제 역할 관리 및 멤버 자격 이해 했으므로 LoginView 컨트롤 ASP.NET 2.0에는이 기능을 사용 하는 방법을 간략하게 설명 있습니다. 앞에서 설명한 대로 LoginView 컨트롤은 기본적으로 두 가지 서식 파일을 포함 하는 템플릿 기반 컨트롤 AnonymousTemplate 및는 LoggedInTemplate 합니다. 내 LoginView 하는 작업 대화 상자 (아래 참조) 링크는 RoleGroups 편집할 수 있습니다.


![](membership/_static/image9.jpg)

**그림 9**


각 RoleGroup 개체 RoleGroup에 적용 되는 어떤 역할을 정의 하는 문자열의 배열을 포함 합니다. 새 RoleGroup LoginView 컨트롤을 추가 하려면 RoleGroups 편집 링크를 클릭 합니다. 위의 그림에서 관리자에 대 한 새 RoleGroup 추가 했지만 볼 수 있습니다. 해당 RoleGroup를 선택 하 여 (RoleGroup[0]) 뷰 드롭다운 목록에서 I 템플릿을 구성할 수만 관리자 역할의 멤버에 게 표시 되는 합니다. 아래 그림에서는 Sales 역할 및 배포 역할의 멤버에 적용 되는 새 RoleGroup 추가 했습니다. 두 번째 RoleGroup LoginView 작업 대화 상자에서 뷰 드롭다운 목록에 추가 하 고 해당 서식 파일에 추가 하는 아무 것도 Sales 또는 배포의 모든 사용자가 볼 수 있습니다 역할입니다.


![](membership/_static/image10.jpg)

**그림 10**


## <a name="overriding-the-existing-membership-provider"></a>기존 멤버 자격 공급자를 재정의합니다.

여러 가지 방법으로 ASP.NET 멤버 자격 기능을 확장할 수 있습니다. 우선, 여기에서 상속 하 고 해당 메서드를 재정의 하 여 SqlMembershipProvider 클래스의 기존 기능을 분명히 변경할 수 있습니다. 예를 들어 사용자를 만들 때 사용자 고유의 기능을 구현 하려면 다음과 같이 SqlMembershipProvider에서 상속 되는 고유한 클래스를 만들 수 있습니다.

[!code-csharp[Main](membership/samples/sample5.cs)]

공급자 (예를 들어 Access 데이터베이스에 멤버 자격 정보를 저장)를 직접 만들려고 한다고 하는 반면에, 경우에 사용자 고유의 공급자를 만들 수 있습니다.

## <a name="creating-your-own-membership-provider"></a>직접 멤버 자격 공급자 만들기

직접 멤버 자격 공급자를 만들려면 먼저 MembershipProvider 클래스에서 상속 되는 클래스를 만드는 해야 합니다. VB.NET를 사용 하는 경우 Visual Studio 2005는 모든 재정의 해야 하는 방법에 대 한 스텁을 추가 합니다. C#, 해당 최대 스텁이 추가할 수 있습니다 사용 하는 경우.

다음 재정의 해야 합니다.

- ApplicationName 속성
- ChangePassword 함수
- ChangePasswordQuestionAndAnswer function
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
- MinRequiredNonAlphanumericCharacters property
- MinRequiredPasswordLength 속성
- PasswordAttemptWindow 속성
- PasswordFormat 속성
- PasswordStrengthRegularExpression 속성
- RequiresQuestionAndAnswer 속성
- RequiresUniqueEmail 속성
- ResetPassword 함수
- 사용자 함수를 잠금 해제
- 하기 위한 함수
- ValidateUser 함수

Thats C# 개발자로 구현 하는 목록입니다. Vb.net에서 모든 구현 없이 클래스를 만들고 다음 C# 코드를 변환할.NET Reflector 또는 유사한 도구를 사용 하는 보다 쉽게 찾을 수 있습니다.

연결 문자열 및 기타 속성을 Initialize 메서드가 기본값으로 설정 되어야 합니다. (Initialize 메서드는 발생 공급자가 있는 경우 런타임 시 로드 합니다.) Initialize 메서드를 두 번째 매개 변수 형식이 System.Collections.Specialized.NameValueCollection 고에 대 한 참조는 &lt;추가&gt; web.config 파일에서 사용자 지정 공급자와 연결 된 요소입니다. 해당 항목은 다음과 같습니다.

[!code-xml[Main](membership/samples/sample6.xml)]

Initialize 메서드의 예를 들면 다음과 같습니다.

[!code-csharp[Main](membership/samples/sample7.cs)]

로그인 폼을 제출할 때 사용자를 확인 하기 위해 ValidateUser 메서드를 사용 해야 합니다. 이 메서드는 Login 컨트롤에서 로그인 단추를 클릭할 때 발생 합니다. 이 방법에서는 사용자 조회를 수행 하는 코드를 배치 합니다.

볼 수 있듯이 어렵지 않습니다 직접 멤버 자격 공급자를 작성 하 고의 ASP.NET 2.0이 강력한 기능을 확장할 수 있습니다.
