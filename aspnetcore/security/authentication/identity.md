---
title: "ASP.NET Core Identity 소개"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램과 함께 Id를 사용 합니다. 암호 요구 사항 설정 (RequireDigit, RequiredLength, RequiredUniqueChars 등) 포함 되어 있습니다."
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/identity
ms.openlocfilehash: a84c5f1d4cf802ee0c4116d2a02bdbfbab9aa72b
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="introduction-to-identity-on-aspnet-core"></a>ASP.NET Core Identity 소개

작성자:[Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway [Erik Reitan](https://github.com/Erikre), [Steve Smith](https://ardalis.com/)

ASP.NET Core Identity는 응용 프로그램에 로그인 기능을 추가할 수 있는 멤버십 시스템입니다. 사용자는 계정을 생성한 다음 사용자 이름과 비밀번호를 사용해서 로그인하거나 Facebook, Google, Microsoft Account, Twitter 같은 외부 로그인 공급자를 사용할 수 있습니다.

ASP.NET Core Identity는 SQL Server 데이터베이스에 사용자 이름, 비밀번호 및 프로필 정보를 저장하도록 구성할 수 있습니다. 또는 Azure 테이블 저장소 같은 사용자 고유의 영구 저장소를 사용할 수도 있습니다. 이 문서는 Visual Studio 및 CLI를 사용하는 경우에 대한 지침을 모두 포함합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [(다운로드 방법)](https://docs.microsoft.com/aspnet/core/tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a>Identity 개요

본문에서는 ASP.NET Core Identity를 이용해서 사용자를 등록하고, 로그인하고, 로그아웃하는 기능을 추가하는 방법을 살펴봅니다. ASP.NET Core Identity를 이용해서 응용 프로그램을 생성하는 보다 상세한 지침은 본문의 마지막 섹션인 다음 단계 섹션을 참고하시기 바랍니다.

1.  개별 사용자 계정으로 새로운 ASP.NET Core 웹 응용 프로그램 생성하기.

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

2.  Identity 서비스를 구성하고 `Startup`에서 미들웨어 추가하기.

    Identity 서비스는 `Startup` 클래스의 `ConfigureServices` 메서드에서 응용 프로그램에 추가됩니다:

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]
    
    이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.
    
    `Configure` 메서드에서 `UseAuthentication` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다. `UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)
    
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]
    
    이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.
    
    `Configure` 메서드에서 `UseIdentity` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다. `UseIdentity`는 요청 파이프라인에 쿠키 기반의 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.
        
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]
    
    ---
     
    응용 프로그램 시작 과정에 대한 더 자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.

3.  사용자 생성.

    응용 프로그램을 시작 하 고을 클릭는 **등록** 링크 합니다.

    처음이이 작업을 수행 하는 경우 마이그레이션을 실행 하는 데 필요한 수 있습니다. 응용 프로그램 하 라는 메시지가 표시 **적용 마이그레이션**합니다. 필요한 경우 페이지를 새로 고칩니다.
    
    ![마이그레이션 웹 페이지를 적용 합니다.](identity/_static/apply-migrations.png)
    
    또는 영구 데이터베이스 없이 응용 프로그램과 함께 ASP.NET Core Id를 사용 하 여 메모리 내 데이터베이스를 사용 하 여 테스트할 수 있습니다. 메모리 내 데이터베이스를 사용 하려면 추가 ``Microsoft.EntityFrameworkCore.InMemory`` 앱 패키지 및 응용 프로그램의 호출을 수정 ``AddDbContext`` 에 ``ConfigureServices`` 다음과 같습니다.

    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
    ```
    
    사용자가 클릭할 때는 **등록** 링크는 ``Register`` 에서 동작이 호출 될 ``AccountController``합니다. ``Register`` 동작 호출 하 여 사용자를 만듭니다 `CreateAsync` 에 `_userManager` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여):
 
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

    에 대 한 호출 사용자가 로그인 된 사용자가 성공적으로 만들어진 경우 ``_signInManager.SignInAsync``합니다.

    **참고:** 참조 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 등록 시 즉시 로그인을 방지 하는 단계에 대 한 합니다.
 
4.  로그인.
 
    사용자가 클릭 하 여 로그인 할 수는 **로그인** 사이트의 맨 위에 링크 될 수 있습니다 이동 하 게 될 로그인 페이지에 권한 부여를 요구 하는 사이트의 일부에 액세스 하려는 경우 또는 합니다. 사용자가 로그인 페이지에 폼을 제출는 ``AccountController`` ``Login`` 작업을 호출 합니다.

    ``Login`` 동작 호출 ``PasswordSignInAsync`` 에 ``_signInManager`` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여).

    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]
 
    기본 ``Controller`` 클래스가 노출 한 ``User`` 컨트롤러 메서드에서 액세스할 수 있는 속성입니다. 예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다. 자세한 내용은 참조 [권한 부여](xref:security/authorization/index)합니다.
 
5.  로그 아웃 합니다.
 
    클릭 하 고 **로그 아웃** 호출 연결는 `LogOut` 동작 합니다.
 
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]
 
    앞의 코드 호출 위에 `_signInManager.SignOutAsync` 메서드. `SignOutAsync` 메서드 쿠키에 저장 하는 사용자의 클레임을 지웁니다.
 
<a name="pw"></a>
6.  구성입니다.

    Id는 응용 프로그램의 시작 클래스에서 재정의 될 수 있는 몇 가지 기본 동작에 있습니다. `IdentityOptions` 기본 동작을 사용 하는 경우 구성할 필요가 없습니다. 다음 코드는 여러 가지 암호 강도 옵션을 설정합니다.

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)
    
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-33)]

    ---
    
    Id를 구성 하는 방법에 대 한 자세한 내용은 참조 [구성 Identity](xref:security/authentication/identity-configuration)합니다.
    
    기본 키의 데이터 형식을 구성할 수 참조 [Id 구성 기본 키 데이터 형식이](xref:security/authentication/identity-primary-key-configuration)합니다.
 
7.  데이터베이스를 봅니다.

    앱 (Windows와 Visual Studio 사용자에 대 한 기본값)는 SQL Server 데이터베이스를 사용 하는 경우에 만든 응용 프로그램 데이터베이스를 볼 수 있습니다. 사용할 수 있습니다 **SQL Server Management Studio**합니다. 또는 Visual Studio에서 선택 **보기** > **SQL Server 개체 탐색기**합니다. 연결할 **(localdb) \MSSQLLocalDB**합니다. 일치 하는 이름을 사용 하 여 데이터베이스 **aspnet-<*프로젝트의 이름*>-<*날짜 문자열* >**  표시 됩니다.

    ![AspNetUsers 데이터베이스 테이블에 대 한 상황에 맞는 메뉴](identity/_static/04-db.png)
    
    데이터베이스 확장 및 해당 **테이블**를 마우스 오른쪽 단추로 클릭 한 다음는 **dbo입니다. AspNetUsers** 테이블을 선택한 **데이터 보기**합니다.

8. Identity 작동 확인

    기본 *ASP.NET Core 웹 응용 프로그램* 프로젝트 템플릿이 필요 없이 응용 프로그램에서 모든 작업에 액세스할 수 있도록 로그인에 있습니다. ASP.NET Identity 작동 하는지 확인 하려면 추가`[Authorize]` 특성을 `About` 의 작업은 `Home` 컨트롤러입니다.
 
    ```cs
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```
    
    # <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

    사용 하 여 프로젝트 실행 **Ctrl** + **F5** 로 이동 하 고는 **에 대 한** 페이지. 인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.

    # <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

    명령 창을 열고 프로젝트의 루트 디렉터리로 이동 포함 된 디렉터리는 `.csproj` 파일입니다. 실행의 [실행 dotnet](/dotnet/core/tools/dotnet-run) 명령을 앱을 실행 하려면:

    ```cs
    dotnet run 
    ```

    검색의 출력에 지정 된 URL의 [dotnet 실행](/dotnet/core/tools/dotnet-run) 명령입니다. URL 가리키는 `localhost` 생성 된 포트 번호를 사용 합니다. 탐색 하 고 **에 대 한** 페이지. 인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.

    ---

## <a name="identity-components"></a>Identity 구성 요소

Id 시스템에 대 한 기본 참조 어셈블리는 `Microsoft.AspNetCore.Identity`합니다. 이 패키지 ASP.NET Core Id에 대 한 인터페이스의 핵심 집합으로 포함 되어 있으며 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`합니다.

이러한 종속성 ASP.NET Core 응용 프로그램의 Id 시스템을 사용 하려면 필요 합니다.

* `Microsoft.AspNetCore.Identity.EntityFrameworkCore` -Identity Entity Framework Core 사용 시 필요한 형식을 포함 합니다.

* `Microsoft.EntityFrameworkCore.SqlServer` -Entity Framework Core는 SQL Server와 같은 관계형 데이터베이스에 대 한 Microsoft의 권장 되는 데이터 액세스 기술입니다. 테스트를 위해 사용할 수 있습니다 `Microsoft.EntityFrameworkCore.InMemory`합니다.

* `Microsoft.AspNetCore.Authentication.Cookies` -앱이 쿠키 기반 인증을 사용할 수 있도록 하는 미들웨어입니다.

## <a name="migrating-to-aspnet-core-identity"></a>ASP.NET Core Id로 마이그레이션

추가 정보 및 기존 본인 마이그레이션하는 방법에 대 한 지침을 참조 저장 [마이그레이션 인증 및 Id](xref:migration/identity)합니다.

## <a name="setting-password-strength"></a>암호 강도 설정합니다.

참조 [구성](#pw) 최소 암호 요구 사항을 설정 하는 샘플입니다.

## <a name="next-steps"></a>다음 단계

* [인증 및 ID 마이그레이션](xref:migration/identity)
* [계정 확인 및 암호 복구](xref:security/authentication/accconfirm)
* [SMS를 사용한 2단계 인증](xref:security/authentication/2fa)
* [Facebook, Google, 및 외부 공급자 인증](xref:security/authentication/social/index)
