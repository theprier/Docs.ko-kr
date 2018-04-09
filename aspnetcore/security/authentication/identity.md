---
title: ASP.NET Core Identity 소개
author: rick-anderson
description: ASP.NET Core 응용 프로그램에서 Identity 사용하기 암호 요구 사항 설정 (RequireDigit, RequiredLength, RequiredUniqueChars 등) 포함 되어 있습니다.
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/identity
ms.openlocfilehash: b3bfae665403162db1fb012fac227275b1dfd6c9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="introduction-to-identity-on-aspnet-core"></a>ASP.NET Core Identity 소개

작성자:[Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway [Erik Reitan](https://github.com/Erikre), [Steve Smith](https://ardalis.com/)

ASP.NET Core Identity는 응용 프로그램에 로그인 기능을 추가할 수 있는 멤버십 시스템입니다. 사용자는 계정을 생성한 다음 사용자 이름과 비밀번호를 사용해서 로그인하거나 Facebook, Google, Microsoft Account, Twitter 같은 외부 로그인 공급자를 사용할 수 있습니다.

ASP.NET Core Identity는 SQL Server 데이터베이스에 사용자 이름, 비밀번호 및 프로필 정보를 저장하도록 구성할 수 있습니다. 또는 Azure 테이블 저장소 같은 사용자 고유의 영구 저장소를 사용할 수도 있습니다. 이 문서는 Visual Studio 및 CLI를 사용하는 경우에 대한 지침을 모두 포함합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [(다운로드 방법)](https://docs.microsoft.com/aspnet/core/tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a>Identity 개요

본문에서는 ASP.NET Core Identity를 이용해서 사용자를 등록하고, 로그인하고, 로그아웃하는 기능을 추가하는 방법을 살펴봅니다. ASP.NET Core Identity를 이용해서 응용 프로그램을 생성하는 보다 상세한 지침은 본문의 마지막 섹션인 다음 단계 섹션을 참고하시기 바랍니다.

1. 개별 사용자 계정으로 새로운 ASP.NET Core 웹 응용 프로그램 생성하기.

   # <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

   Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. 그리고 **ASP.NET Core 웹 응용 프로그램**을 선택한 다음,**확인**을 클릭합니다.

   ![새 프로젝트 대화 상자](identity/_static/01-new-project.png)

   ASP.NET Core 2.x 용 ASP.NET Core**웹 응용 프로그램 (모델-뷰-컨트롤러)**을 선택한 다음 **인증 변경**을 선택합니다.

   ![새 프로젝트 대화 상자](identity/_static/02-new-project.png)

   그러면 인증 방식을 선택할 수 있는 대화 상자가 나타납니다. **개별 사용자 계정**을 선택하고 **확인**을 클릭해서 이전 대화 상자로 돌아갑니다.

   ![새 프로젝트 대화 상자](identity/_static/03-new-project-auth.png)

   이렇게 **개별 사용자 계정**을 선택하면 Visual Studio에게 프로젝트 템플릿의 일부로 인증에 필요한 모델, 뷰 모델, 뷰, 컨트롤러 및 기타 자산을 생성하도록 지시합니다.

   # <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

   .NET Core CLI를 사용하는 경우, ``dotnet new mvc --auth Individual`` 명령으로 새로운 프로젝트를 생성합니다. 이 명령은 Visual Studio가 생성하는 것과 동일한 Identity 템플릿 코드를 사용하는 새로운 프로젝트를 생성합니다.

   생성된 프로젝트에는 [Entity Framework Core](https://docs.microsoft.com/ef/)를 이용해서 SQL Server에 Identity 데이터와 스키마를 저장하는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 패키지가 포함되어 있습니다.

   ---

2. Identity 서비스를 구성하고 `Startup`에서 미들웨어 추가하기.

   Identity 서비스는 `Startup` 클래스의 `ConfigureServices` 메서드에서 응용 프로그램에 추가됩니다:

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.

   `Configure` 메서드에서 `UseAuthentication` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다. `UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.

   `Configure` 메서드에서 `UseIdentity` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다. `UseIdentity`는 요청 파이프라인에 쿠키 기반의 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

   * * *
   응용 프로그램 시작 과정에 대한 더 자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.

3. 사용자 생성.

   응용 프로그램을 실행한 다음, **Register** 링크를 클릭합니다.

   이 작업을 처음 수행하는 경우, 마이그레이션을 실행해야 할 수도 있습니다. 그럴 경우, **이그레이션을 수행** 하라는 메시지가 응용 프로그램에 표시됩니다. 필요한 경우 페이지를 새로 고침합니다.

   ![마이그레이션 웹 페이지를 적용합니다.](identity/_static/apply-migrations.png)

   또는 영구적인 데이터베이스 없이 메모리 내 데이터베이스를 이용해서 응용 프로그램과 ASP.NET Core Identity를 테스트할 수도 있습니다. 메모리 내 데이터베이스를 사용하려면 응용 프로그램에 ``Microsoft.EntityFrameworkCore.InMemory`` 패키지를 추가하고, 응용 프로그램이 ``ConfigureServices``에서 ``AddDbContext``를 호출하는 부분을 다음과 같이 수정합니다:

   ```csharp
   services.AddDbContext<ApplicationDbContext>(options =>
       options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
   ```

   사용자가 **Register** 링크를 클릭하면 ``AccountController`` 에서 ``Register`` 액션이 호출됩니다. ``Register`` 액션은 `_userManager` 개체의 (종속성 주입으로 ``AccountController``에 제공된) `CreateAsync`를 호출해서 사용자를 생성합니다:

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

   사용자가 정상적으로 생성되면 ``_signInManager.SignInAsync`` 가 호출되어 사용자가 즉시 로그인됩니다.

   **참고:** 사용자 등록 즉시 로그인을 방지하는 방법은 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 을 참고하시기 바랍니다.

4. 로그인

   사용자는 사이트 상단의 **Log in** 링크를 클릭해서 로그인할 수 있으며, 사이트에서 권한 부여가 필요한 페이지에 접근하려고 시도할 경우 Login 페이지로 이동하게 됩니다. 사용자가 Login 페이지의 양식을 제출하면 ``AccountController``의 ``Login`` 액션이 호출됩니다.

   ``Login`` 액션은 ``_signInManager`` 개체의 (종속성 주입으로 ``AccountController`` 에 제공된) ``PasswordSignInAsync``를 호출합니다. 

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

   기본 ``Controller`` 클래스는 컨트롤러의 메서드에서 접근할 수 있는 ``User`` 속성을 제공합니다. 예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다. 자세한 내용은 참조 [권한 부여](xref:security/authorization/index)합니다.

5. 로그아웃

   **LogOut** 링크를 클릭하면 `LogOut` 액션이 호출됩니다.

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   위의 코드는 `_signInManager.SignOutAsync` 메서드를 호출합니다. `SignOutAsync`메서드는 쿠키에 저장된 사용자의 클레임을 삭제합니다.

<a name="pw"></a>
6. 구성

   Identity는 응용 프로그램의 시작 클래스에서 재지정할 수 있는 몇 가지 기본적인 동작을 갖고 있습니다. 기본 동작을 사용하고자 하는 경우에는 `IdentityOptions` 를 구성할 필요가 없습니다. 다음 코드는 여러 가지 암호 강도 옵션을 설정합니다.

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-33)]

   * * *
   Identity를 구성하는 보다 자세한 방법은 [Identity 구성하기](xref:security/authentication/identity-configuration)를 참고하시기 바랍니다.

   기본 키의 데이터 형식도 구성 가능합니다. [Identity 기본 키 데이터 형식 구성하기](xref:security/authentication/identity-primary-key-configuration)를 참고하시기 바랍니다. 

7. 데이터베이스 살펴보기

   응용 프로그램에서 SQL Server 데이터베이스를 사용할 경우 (Windows 및 Visual Studio 사용자에 대한 기본값), 응용 프로그램이 생성한 데이터베이스를 확인할 수 있습니다. 이때 **SQL Server Management Studio** 를 사용할 수 있습니다 또는 Visual Studio에서 **보기**  >  **SQL Server 개체 탐색기**를 선택합니다. 그리고 **(localdb) \MSSQLLocalDB**에 연결합니다. 그러면 **aspnet-<*프로젝트명*>-<*날짜 문자열*>** 형태의 이름을 가진 데이터베이스가 표시됩니다.

   ![AspNetUsers 데이터베이스 테이블에 대한 컨텍스트 메뉴](identity/_static/04-db.png)

   데이터베이스와 그 **테이블** 들을 확장하고, **dbo.AspNetUsers** 테이블을 마우스 오른쪽 버튼으로 클릭한 다음, **데이터 보기**를 선택합니다.

8. Identity 동작 확인하기

    기본 *ASP.NET Core 웹 응용 프로그램* 프로젝트 템플릿은 사용자가 로그인하지 않더라도 응용 프로그램의 모든 액션에 접근할 수 있습니다. 정상적으로 ASP.NET Identity가 동작하는지 확인해보려면 `Home` 컨트롤러의 `About` 액션에 `[Authorize]` 특성을 추가합니다.

    ```cs
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```

    # <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

    **Ctrl**  +  **F5** 키를 눌러서 프로젝트를 실행하고 **About** 페이지로 이동합니다. 이제 인증된 사용자만 **About** 페이지에 액세스할 수 있으므로 사용자가 로그인하거나 등록할 수 있도록 로그인 페이지로 리디렉션됩니다.

    # <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

    명령 창을 열고 `.csproj` 파일이 위치한 프로젝트의 루트 디렉터리로 이동합니다. 실행의 [실행 dotnet](/dotnet/core/tools/dotnet-run) 명령을 앱을 실행 하려면:

    ```cs
    dotnet run 
    ```

    검색의 출력에 지정 된 URL의 [dotnet 실행](/dotnet/core/tools/dotnet-run) 명령입니다. 이 URL은 생성된 포트 번호가 지정된 `localhost`를 가리켜야 합니다. 브라우저에서 **About** 페이지로 이동합니다. 이제 인증된 사용자만 **About** 페이지에 액세스할 수 있으므로 사용자가 로그인하거나 등록할 수 있도록 로그인 페이지로 리디렉션됩니다.

    ---

## <a name="identity-components"></a>Identity 구성 요소

Identity 시스템의 기본 참조 어셈블리는 `Microsoft.AspNetCore.Identity` 입니다. ASP.NET Core Identity에 대한 주요 인터페이스 모음을 포함하고 있는 이 패키지는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`에 포함되어 있습니다.

ASP.NET Core 응용 프로그램에서 Identity 시스템을 사용하려면 다음과 같은 종속성들이 필요합니다:

* `Microsoft.AspNetCore.Identity.EntityFrameworkCore` -Entity Framework Core로 Identity를 사용하는데 필요한 형식들을 포함하고 있습니다.

* `Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core는 SQL Server와 같은 관계형 데이터베이스에 대한 Microsoft의 권장 데이터 액세스 기술입니다. 테스트 목적으로 대신 `Microsoft.EntityFrameworkCore.InMemory` 를 사용할 수도 있습니다.

* `Microsoft.AspNetCore.Authentication.Cookies` -응용 프로그램이 쿠키 기반의 인증을 사용할 수 있게 해주는 미들웨어입니다.

## <a name="migrating-to-aspnet-core-identity"></a>ASP.NET Identity로 마이그레이션하기

추가 정보 및 기존 본인 마이그레이션하는 방법에 대 한 지침을 참조 저장 [마이그레이션할 인증 및 Id](xref:migration/identity)합니다.

## <a name="setting-password-strength"></a>암호 강도 설정합니다.

참조 [구성](#pw) 최소 암호 요구 사항을 설정 하는 샘플입니다.

## <a name="next-steps"></a>다음 단계

* [인증 및 Id 마이그레이션](xref:migration/identity)
* [계정 확인 및 비밀번호 복구](xref:security/authentication/accconfirm)
* [SMS를 이용한 2단계 인증](xref:security/authentication/2fa)
* [Facebook, Google 및 기타 외부 공급자를 이용한 인증 활성화](xref:security/authentication/social/index)
