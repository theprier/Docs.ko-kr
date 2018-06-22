---
title: ASP.NET 및 ASP.NET Core와 앱 간에 쿠키를 공유
author: rick-anderson
description: ASP.NET 간에 인증 쿠키를 공유 하는 방법에 알아봅니다 4.x 및 ASP.NET Core 응용 프로그램입니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/19/2017
uid: security/cookie-sharing
ms.openlocfilehash: 2636688fa50fb36a8cbd07549e8038474ffa30ca
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278468"
---
# <a name="share-cookies-among-apps-with-aspnet-and-aspnet-core"></a>ASP.NET 및 ASP.NET Core와 앱 간에 쿠키를 공유

여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Luke Latham](https://github.com/guardrex)

웹 사이트는 자주 함께 작동 하는 개별 웹 응용 프로그램의 구성 됩니다. 환경을 제공 하기 위해 single sign on (SSO), 사이트 내에서 웹 앱 인증 쿠키를 공유 해야 합니다. 이런 시나리오에 대응하기 위해서, 데이터 보호 스택은 Katana 쿠키 인증 및 ASP.NET Core 쿠키 인증 티켓의 공유를 지원합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 샘플에서는 쿠키 인증을 사용 하는 세 개의 앱 간에 공유 되는 쿠키를 보여 줍니다.

* 사용 하지 않고 ASP.NET 코어 2.0 Razor 페이지 앱 [ASP.NET 코어 Id](xref:security/authentication/identity)
* ASP.NET Core Id 가진 ASP.NET Core 2.0 MVC 응용 프로그램
* ASP.NET Id를 가진 ASP.NET Framework 4.6.1 MVC 응용 프로그램

다음에 나오는 예제:

* 인증 쿠키 이름을 설정 하는 일반적인 값으로 `.AspNet.SharedCookie`합니다.
* `AuthenticationType` 로 설정 된 `Identity.Application` 명시적으로 나 기본적으로 합니다.
* 일반적인 응용 프로그램 이름을 사용 하는 데이터 보호 키를 공유 하는 데이터 보호 시스템을 사용 하도록 설정 하려면 (`SharedCookieApp`).
* `Identity.Application` 인증 체계도 사용 됩니다. 모든 체계를 사용, 지속적으로 사용 해야 *팀 내 및 간* 기본 체계 또는 명시적으로 설정 하 여 공유 쿠키 앱. 암호화 및 일관 된 체계를 사용 하 여 앱 간에 해야 하므로 쿠키를 암호 해독 하는 경우에 구성표가 사용 됩니다.
* 공통 [데이터 보호 키](xref:security/data-protection/implementation/key-management) 저장소 위치가 사용 됩니다. 샘플 응용 프로그램 폴더를 사용 하 여 *KeyRing* 데이터 보호 키를 저장할 솔루션의 루트에 있습니다.
* ASP.NET Core 응용 프로그램에서 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 키 저장소 위치를 설정 하는 데 사용 됩니다. [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 공통 공유 응용 프로그램 이름을 구성 하는 데 사용 됩니다.
* .NET Framework 응용 프로그램에서 쿠키 인증 미들웨어는 구현을 사용 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)합니다. `DataProtectionProvider` 암호화 및 인증 쿠키 페이로드 데이터의 암호 해독에 대 한 데이터 보호 서비스를 제공합니다. `DataProtectionProvider` 인스턴스 응용 프로그램의 다른 부분에서 사용 되는 데이터 보호 시스템에서 격리 됩니다.
  * [DataProtectionProvider.Create (System.IO.DirectoryInfo, 작업\<IDataProtectionBuilder >)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_System_Action_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder__) 허용는 [DirectoryInfo](/dotnet/api/system.io.directoryinfo) 데이터 보호에 대 한 키 저장소에 대 한 위치를 지정 합니다. 경로 제공 하는 샘플 응용 프로그램은 *KeyRing* 폴더 `DirectoryInfo`합니다. [DataProtectionBuilderExtensions.SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionBuilderExtensions_SetApplicationName_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_) 일반적인 응용 프로그램 이름을 설정 합니다.
  * [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) 를 사용하려면 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet 패키지가 필요합니다. ASP.NET Core 2.1 및 이상 앱에 대 한이 패키지를 가져오려면 참조는 [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)합니다. .NET Framework를 대상으로 하는 경우에 대 한 패키지 참조 추가 `Microsoft.AspNetCore.DataProtection.Extensions`합니다.

## <a name="share-authentication-cookies-among-aspnet-core-apps"></a>ASP.NET Core 응용 프로그램 간에 인증 쿠키를 공유 합니다.

사용할 경우 ASP.NET Core Id:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

에 `ConfigureServices` 메서드를 사용 하 여는 [ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie) 확장 메서드를 쿠키에 대 한 데이터 보호 서비스를 설정 합니다.

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

데이터 보호 키와 앱 이름을 앱 간에 공유 되어야 합니다. 샘플 응용 프로그램에서 `GetKeyRingDirInfo` 에 공용 키 저장소 위치를 반환 합니다.는 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 메서드. 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 공통 공유 응용 프로그램 이름을 구성 하려면 (`SharedCookieApp` 샘플에서). 자세한 내용은 참조 [데이터 보호 구성](xref:security/data-protection/configuration/overview)합니다.

참조는 *CookieAuthWithIdentity.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

에 `Configure` 메서드를 사용 하 여는 [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions) 를 설정 하려면:

* 쿠키에 대 한 데이터 보호 서비스입니다.
* `AuthenticationScheme` ASP.NET에 맞게 4.x 합니다.

```csharp
app.AddIdentity<ApplicationUser, IdentityRole>(options =>
{
    options.Cookies.ApplicationCookie.AuthenticationScheme = 
        "ApplicationCookie";

    var protectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"));

    options.Cookies.ApplicationCookie.DataProtectionProvider = 
        protectionProvider;

    options.Cookies.ApplicationCookie.TicketDataFormat = 
        new TicketDataFormat(protectionProvider.CreateProtector(
            "Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware", 
            "Cookies", 
            "v2"));
});
```

---

쿠키를 직접 사용 하 여 하는 경우:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]

데이터 보호 키와 앱 이름을 앱 간에 공유 되어야 합니다. 샘플 응용 프로그램에서 `GetKeyRingDirInfo` 에 공용 키 저장소 위치를 반환 합니다.는 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 메서드. 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 공통 공유 응용 프로그램 이름을 구성 하려면 (`SharedCookieApp` 샘플에서). 자세한 내용은 참조 [데이터 보호 구성](xref:security/data-protection/configuration/overview)합니다. 

참조는 *CookieAuth.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
});
```

---

## <a name="encrypting-data-protection-keys-at-rest"></a>미사용 데이터 보호 키를 암호화합니다.

프로덕션 배포에 구성 된 `DataProtectionProvider` DPAPI 또는 X509Certificate 저장 된 상태의 키를 암호화 하 합니다. 참조 [휴지 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest) 자세한 정보에 대 한 합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .ProtectKeysWithCertificate("thumbprint");
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = DataProtectionProvider.Create(
        new DirectoryInfo(@"PATH_TO_KEY_RING"),
        configure =>
        {
            configure.ProtectKeysWithCertificate("thumbprint");
        })
});
```

---

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-apps"></a>ASP.NET 4.x 응용 프로그램과 ASP.NET Core 응용 프로그램 간 인증 쿠키 공유하기

Katana 쿠키 인증 미들웨어를 사용하는 ASP.NET 4.x 응용 프로그램은 ASP.NET Core 쿠키 인증 미들웨어와 호환되는 인증 쿠키를 생성하도록 구성할 수 있습니다. 이렇게 하면 사이트 전체에 원활한 SSO 환경을 제공 하면서 증분 대규모 사이트의 개별 응용 프로그램을 업그레이드 합니다.

응용 프로그램에서 Katana 쿠키 인증 미들웨어를 사용 하는 경우 호출 `UseCookieAuthentication` 프로젝트의 *Startup.Auth.cs* 파일입니다. ASP.NET 4.x 웹 앱 프로젝트는 Visual Studio 2013을 사용 하 여 만든 하 고 나중 Katana 쿠키 인증 미들웨어를 사용 하 여 기본적으로 합니다. 하지만 `UseCookieAuthentication` 오래 되어 ASP.NET Core 응용 프로그램, 호출에 대 한 지원 되지 않는 `UseCookieAuthentication` Katana를 사용 하 여 ASP.NET 4.x 응용 프로그램 쿠키 인증 미들웨어의 유효 합니다.

ASP.NET 4.x 앱.NET Framework 4.5.1을 대상 해야 이상. 그렇지 않으면 필요한 NuGet 패키지 설치에 실패 합니다.

ASP.NET Core 응용 프로그램 및 ASP.NET 4.x 응용 프로그램 간의 인증 쿠키를 공유 하려면 위에서 설명 했 듯이 ASP.NET Core 응용 프로그램을 구성 하 고이 단계를 수행 하 여 ASP.NET 4.x 응용 프로그램 구성:

1. 패키지 설치 [Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/) 각 ASP.NET 4.x 응용 프로그램에 있습니다.

2. *Startup.Auth.cs* 파일에서 `UseCookieAuthentication` 에 대한 호출을 찾고 다음과 같이 수정합니다. ASP.NET Core 쿠키 인증 미들웨어에서 사용 하는 이름과 일치 하도록 쿠키 이름을 변경 합니다. 인스턴스를 제공는 `DataProtectionProvider` 공통 데이터 보호 키 저장소 위치를 초기화 합니다. 응용 프로그램 이름, 쿠키를 공유 하는 모든 앱에서 사용 하는 일반 응용 프로그램 이름으로 설정 되어 있는지 확인 `SharedCookieApp` 샘플 응용 프로그램에서입니다.

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]

참조는 *CookieAuthWithIdentity.NETFramework* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).

인증 형식에 정의 된 형식과 일치 해야 사용자 id를 생성할 때 `AuthenticationType` 사용 하 여 설정 `UseCookieAuthentication`합니다.

*Models/IdentityModels.cs*:

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]

## <a name="use-a-common-user-database"></a>일반 사용자 데이터베이스를 사용 하 여

동일한 사용자 데이터베이스에서 각 앱에 대 한 id 시스템 가리키고 있는지 확인 합니다. 그렇지 않으면 id 시스템 데이터베이스의 정보에 대해 인증 쿠키의 정보와 일치 하려고 할 때 런타임 시 오류를 생성 합니다.
