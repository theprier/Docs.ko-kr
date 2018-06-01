---
title: 계정 확인 및 ASP.NET 코어에서 암호 복구
author: rick-anderson
description: 전자 메일 확인 및 암호 재설정으로 ASP.NET Core 응용 프로그램을 구축 하는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 2/11/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/accconfirm
ms.openlocfilehash: 397d8bf04abf6be811ad8c91d52565251ac61678
ms.sourcegitcommit: 545ff5a632e2281035c1becec1f99137298e4f5c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2018
ms.locfileid: "34688972"
---
# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a>계정 확인 및 ASP.NET 코어에서 암호 복구

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)

이 자습서에서는 전자 메일 확인 및 암호 재설정으로 ASP.NET Core 응용 프로그램을 구축 하는 방법을 보여 줍니다. 이 자습서는 **하지** 시작 항목입니다. 에 대해 잘 알고 있어야 합니다.

* [ASP.NET Core](xref:tutorials/first-mvc-app/start-mvc)
* [인증](xref:security/authentication/index)
* [계정 확인 및 비밀번호 복구](xref:security/authentication/accconfirm)
* [Entity Framework Core](xref:data/ef-mvc/intro)

참조 [이 PDF 파일](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC 1.1 및 2.x 버전에 대 한 합니다.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-new-aspnet-core-project-with-the-net-core-cli"></a>.NET Core CLI 인 새 ASP.NET Core 프로젝트를 만듭니다

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp --auth Individual -o WebPWrecover
cd WebPWrecover
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor --auth Individual -o WebPWrecover
cd WebPWrecover
```

::: moniker-end

* `--auth Individual` 개별 사용자 계정 프로젝트 템플릿을 지정합니다.
* Windows에서 추가 된 `-uld` 옵션입니다. 지정 SQLite 대신 LocalDB를 사용 해야 합니다.
* 실행 `new mvc --help` 도움말을 보려면이 명령에 있습니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

CLI 또는 SQLite를 사용 하는 경우 명령 창에서 다음을 실행 합니다.

```console
dotnet new mvc --auth Individual
```

* `--auth Individual` 개별 사용자 계정 프로젝트 템플릿을 지정합니다.
* Windows에서 추가 된 `-uld` 옵션입니다. 지정 SQLite 대신 LocalDB를 사용 해야 합니다.
* 실행 `new mvc --help` 도움말을 보려면이 명령에 있습니다.

---

또는 Visual Studio와 함께 새 ASP.NET Core 프로젝트를 만들 수 있습니다.

* Visual Studio에서 만드는 새 **웹 응용 프로그램** 프로젝트.
* 선택 **ASP.NET Core 2.0**합니다. **.NET core** 다음 이미지에서 선택한 선택할 수 있지만 **.NET Framework**합니다.
* 선택 **인증 변경** 로 설정 하 고 **개별 사용자 계정**합니다.
* 기본값을 그대로 두고 **저장 된 사용자 계정 앱에서**합니다.

![선택 하는 "개별 사용자 계정 radio"를 표시 하는 새 프로젝트 대화 상자](accconfirm/_static/2.png)

## <a name="test-new-user-registration"></a>새 사용자 등록을 테스트 합니다.

응용 프로그램을 실행, 선택는 **등록** 링크를 선택한 사용자를 등록 합니다. Entity Framework Core 마이그레이션을 실행 하는 지침을 따릅니다. 전자 메일에만 유효성 검사와는 시점에서 [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) 특성입니다. 등록을 제출한 후 응용 프로그램에 로그인 되어 있습니다. 자습서의 뒷부분에 나오는 코드 업데이트 되기 때문 자신의 전자 메일의 유효성을 검사 될 때까지 새 사용자가 로그인 할 수 없습니다.

## <a name="view-the-identity-database"></a>Id 데이터베이스 보기

참조 [SQLite ASP.NET Core MVC 프로젝트에서 작업할](xref:tutorials/first-mvc-app-xplat/working-with-sql) SQLite 데이터베이스를 확인 하는 방법에 대 한 지침은 합니다.

Visual studio의 경우:

* **보기** 메뉴 선택 **SQL Server 개체 탐색기** (SSOX).
* 로 이동 **(localdb) (SQL Server 13) MSSQLLocalDB**합니다. 마우스 오른쪽 단추로 클릭 **dbo입니다. AspNetUsers** > **데이터를 볼**:

![SQL Server 개체 탐색기의 AspNetUsers 테이블에 대 한 상황에 맞는 메뉴](accconfirm/_static/ssox.png)

테이블의 참고 `EmailConfirmed` 필드는 `False`합니다.

응용 프로그램에서 확인 전자 메일을 보낼 때 다음 단계에서이 전자 메일에 다시 사용 수 있습니다. 선택한 행을 마우스 오른쪽 단추로 클릭 **삭제**합니다. 전자 메일 별칭 삭제 쉽게 다음 단계에 있습니다.

---

## <a name="require-https"></a>HTTPS가 필요

참조 [HTTPS가 필요한](xref:security/enforcing-ssl)합니다.

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a>전자 메일 확인이 필요

새 사용자 등록의 전자 메일을 확인 하는 것이 좋습니다. 다른 사람을 가장 하지 하는 것을 확인 하는 데 도움이 확인 전자 메일 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일). 토론 포럼을 가지 며 하지 못하도록 하려는 경우를 가정해 볼 "yli@example.com로 등록" 에서"nolivetto@contoso.com." 전자 메일 확인 하지 않고 "nolivetto@contoso.com" 응용 프로그램에서 원치 않는 전자 메일을 받을 수 있습니다. 사용자는 실수로으로 등록 된다고 가정 합니다 "ylo@example.com" "yli"의 잘못 된 철자를 발견 하지 않은 합니다. 앱이 올바른 전자 메일에 없는 때문에 암호 복구를 사용할 수 없게. 전자 메일 확인에서 봇만 제한 된 보호를 제공합니다. 전자 메일 확인 많은 전자 메일 계정 가진 악의적인 사용자 로부터 보호를 제공 하지 않습니다.

일반적으로 새 사용자는 확인 된 전자 메일을 갖기 전에 웹 사이트에 데이터를 게시 하는 것을 방지 하려고 합니다.

업데이트 `ConfigureServices` 확인 된 전자 메일을 요구 하도록 합니다.

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet1&highlight=12-17)]

`config.SignIn.RequireConfirmedEmail = true;` 등록된 한 사용자의 전자 메일이 확인 될 때까지에 로그인 하지 못하도록 방지 합니다.

### <a name="configure-email-provider"></a>전자 메일 공급자를 구성 합니다.

이 자습서에서는 SendGrid 전자 메일을 보내는 데 사용 됩니다. SendGrid 계정 및 전자 메일을 보내는 키 필요. 다른 전자 메일 공급자를 사용할 수 있습니다. ASP.NET Core 2.x 포함 `System.Net.Mail`, 응용 프로그램에서 전자 메일을 보낼 수 있습니다. 전자 메일을 보내는 SendGrid 또는 다른 전자 메일 서비스를 사용 하는 것이 좋습니다. SMTP 보안을 설정 하 고 올바르게 설정 하기가 어렵습니다.

[옵션 패턴](xref:fundamentals/configuration/options) 사용자 계정 및 키 설정에 액세스 하는 데 사용 됩니다. 자세한 내용은 참조 [구성](xref:fundamentals/configuration/index)합니다.

전자 메일 보안 키를 인출 하는 클래스를 만듭니다. 이 샘플은 `AuthMessageSenderOptions` 클래스에 만들어집니다는 *Services/AuthMessageSenderOptions.cs* 파일:

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/AuthMessageSenderOptions.cs?name=snippet1)]

설정의 `SendGridUser` 및 `SendGridKey` 와 [암호 관리자 도구](xref:security/app-secrets)합니다. 예를 들어:

```console
C:\WebAppl\src\WebApp1>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

Windows에서는 암호 관리자에 있는 키/값 쌍을 저장 한 *secrets.json* 파일에 `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` 디렉터리입니다.

콘텐츠는 *secrets.json* 파일이 암호화 되지 않습니다. *secrets.json* 파일은 다음과 같습니다 (의 `SendGridKey` 값 제거 되었습니다.)

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```

### <a name="configure-startup-to-use-authmessagesenderoptions"></a>AuthMessageSenderOptions를 사용 하는 시작 구성

추가 `AuthMessageSenderOptions` 끝날 때 서비스 컨테이너에는 `ConfigureServices` 에서 메서드는 *Startup.cs* 파일:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet2&highlight=28)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](accconfirm/sample/WebApp1/Startup.cs?name=snippet1&highlight=26)]

---

### <a name="configure-the-authmessagesender-class"></a>AuthMessageSender 클래스 구성

이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. [SendGrid](https://sendgrid.com/), 하지만 SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다.

설치는 `SendGrid` NuGet 패키지:

* 명령줄:

    `dotnet add package SendGrid`

* 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

  `Install-Package SendGrid`

참조 [SendGrid를 무료로 시작](https://sendgrid.com/free/) 무료 SendGrid 계정을 등록할 수 있습니다.

#### <a name="configure-sendgrid"></a>SendGrid를 구성 합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

SendGrid를 구성 하려면 코드에서 다음과 같은 추가 *Services/EmailSender.cs*:

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/EmailSender.cs)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

* 에 코드를 추가 *Services/MessageServices.cs* SendGrid를 구성 하는 다음과 비슷합니다.

[!code-csharp[](accconfirm/sample/WebApp1/Services/MessageServices.cs)]

---

## <a name="enable-account-confirmation-and-password-recovery"></a>계정 확인 및 암호 복구 사용

서식 파일에는 계정 확인 및 암호 복구를 위한 코드가 있습니다. 찾을 `OnPostAsync` 메서드에서 *Pages/Account/Register.cshtml.cs*합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

새로 등록 된 사용자가 있는 다음 줄을 주석 처리에 자동으로 로그온에서 함:

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

전체 메서드 강조 표시 하는 변경 된 줄으로 표시 됩니다.

[!code-csharp[](accconfirm/sample/WebPWrecover/Pages/Account/Register.cshtml.cs?highlight=16&name=snippet_Register)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

계정 확인을 사용 하려면 다음 코드를 주석 처리 제거:

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=16-25&name=snippet_Register)]

**참고:** 코드 때문에 새로 등록 된 사용자의 다음 줄을 주석 처리에 자동으로 로그온 합니다.

```csharp
//await _signInManager.SignInAsync(user, isPersistent: false);
```

코드의 주석 처리 하 여 암호 복구를 사용 하도록 설정 된 `ForgotPassword` 의 동작 *Controllers/AccountController.cs*:

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=17-23&name=snippet_ForgotPassword)]

Form 요소에 주석 처리 제거 *Views/Account/ForgotPassword.cshtml*합니다. 제거 하려는 경우도 `<p> For more information on how to enable reset password ... </p>` 이 문서에 대 한 링크를 포함 하는 요소입니다.

[!code-cshtml[](accconfirm/sample/WebApp1/Views/Account/ForgotPassword.cshtml?highlight=7-10,12,28)]

---

## <a name="register-confirm-email-and-reset-password"></a>등록 전자 메일을 확인 하 고 암호를 다시 설정

웹 응용 프로그램을 실행 하 고 계정 확인 및 암호 복구 흐름을 테스트 합니다.

* 응용 프로그램을 실행 하 고 새 사용자 등록

  ![웹 응용 프로그램 계정 등록 보기](accconfirm/_static/loginaccconfirm1.png)

* 계정 확인 링크에 대 한 전자 메일을 확인 합니다. 참조 [전자 메일을 디버그](#debug) 전자 메일을 얻지 못한 경우.
* 사용자의 전자 메일 확인에 대 한 링크를 클릭 합니다.
* 전자 메일 및 암호를 로그인 합니다.
* 로그 오프 합니다.

### <a name="view-the-manage-page"></a>관리 페이지 보기

브라우저에서 자신의 사용자 이름을 선택: ![사용자 이름으로 브라우저 창](accconfirm/_static/un.png)

사용자 이름을 보려면 탐색 모음을 확장 해야 할 수 있습니다.

![탐색 모음](accconfirm/_static/x.png)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

관리 페이지에 표시 됩니다는 **프로필** 탭이 선택 되어 있습니다. **전자 메일** 확인 전자 메일을 나타내는 확인란을 보여 줍니다.

![관리 페이지](accconfirm/_static/rick2.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

이이 자습서의 뒷부분에 나오는 다룹니다.
![관리 페이지](accconfirm/_static/rick2.png)

---

### <a name="test-password-reset"></a>테스트 암호 재설정

* 로그인 되어 있는 경우 선택 **로그 아웃**합니다.
* 선택 된 **로그인** 연결 하 고 선택의 **암호를 잊으셨나요?** 링크 합니다.
* 계정 등록에 사용한 전자 메일을 입력 합니다.
* 암호를 다시 설정에 대 한 링크가 포함 된 메일이 전송 됩니다. 전자 메일을 확인 하 고 암호를 다시 설정에 대 한 링크를 클릭 합니다. 암호가 성공적으로 다시 설정, 전자 메일 및 새 암호를 사용 하 여 기록할 수 있습니다.

<a name="debug"></a>

### <a name="debug-email"></a>전자 메일을 디버그

전자 메일 작업을 가져올 수 없습니다 하는 경우:

* 만들기는 [전자 메일을 보내는 콘솔 응용 프로그램](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html)합니다.
* 검토는 [전자 메일 작업](https://sendgrid.com/docs/User_Guide/email_activity.html) 페이지.
* 스팸 폴더를 확인 합니다.
* 다른 전자 메일 별칭에는 다른 전자 메일 공급자 (Microsoft, Yahoo, Gmail 등)를 시도 하십시오.
* 다른 전자 메일 주소로 보내 보십시오.

**보안 모범 사례** 를 **하지** 테스트 및 개발에서 생산 암호를 사용 합니다. Azure에 응용 프로그램을 게시 하는 경우에 Azure 웹 앱 포털에서 응용 프로그램 설정으로 SendGrid 암호를 설정할 수 있습니다. 구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.

## <a name="combine-social-and-local-login-accounts"></a>공유 및 로컬 로그인 계정을 결합합니다

이 섹션을 완료 하려면 외부 인증 공급자를 먼저 활성화 해야 합니다. 참조 [Facebook, Google, 및 외부 공급자 인증](xref:security/authentication/social/index)합니다.

사용자 전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다. 그러나 다음 순서로 "RickAndMSFT@gmail.com"; 로컬 로그인으로 처음 만들어질를 만들어 계정을 소셜 로그인으로 먼저, 다음 로컬 로그인을 추가 합니다.

![웹 응용 프로그램: RickAndMSFT@gmail.com 인증 된 사용자](accconfirm/_static/rick.png)

클릭는 **관리** 링크 합니다. 이 계정에 연결 된 참고 0 외부 (소셜 로그인)

![보기를 관리](accconfirm/_static/manage.png)

다른 로그인 서비스에 대 한 링크를 클릭 하 고 응용 프로그램 요청을 수락 합니다. 다음 그림에서는 Facebook 외부 인증 공급자입니다.

![Facebook을 나열 하 여 외부 로그인 보기를 관리 합니다.](accconfirm/_static/fb.png)

두 개의 계정은 결합 되었습니다. 두 계정으로 로그온 할 수 있습니다. 쓰지만 대개를 분실 했다고 액세스 소셜 자신의 계정으로 되거나 자신의 소셜 로그인 인증 서비스가 다운 된 경우 로컬 계정을 추가 하려면 사용자가 할 수 있습니다.

## <a name="enable-account-confirmation-after-a-site-has-users"></a>사이트에 사용자가 만든 후 계정 확인을 사용 하도록 설정

사이트에서 사용할 수 있도록 계정 확인 사용자와 모든 기존 사용자가 잠급니다. 자신의 계정을 확인 하지 때문에 기존 사용자가 잠겨 있습니다. 사용자 잠금 종료를 해결 하려면 다음 방법 중 하나를 사용 합니다.

* 기존의 모든 사용자로 확인 되 고 표시 하도록 데이터베이스를 업데이트
* 기존 사용자를 확인 합니다. 예를 들어 일괄 처리 send 확인 링크가 포함 된 전자 메일입니다.
