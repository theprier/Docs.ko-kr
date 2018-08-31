---
title: ASP.NET 및 ASP.NET Core를 사용 하 여 앱 간 쿠키 공유
author: rick-anderson
description: ASP.NET 중에서 인증 쿠키를 공유 하는 방법을 알아봅니다 4.x 및 ASP.NET Core 앱.
ms.author: riande
ms.custom: mvc
ms.date: 01/19/2017
uid: security/cookie-sharing
ms.openlocfilehash: afb0405ea87a6239c3017ba0a59a22527a817feb
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312284"
---
# <a name="share-cookies-among-apps-with-aspnet-and-aspnet-core"></a>ASP.NET 및 ASP.NET Core를 사용 하 여 앱 간 쿠키 공유

하 여 [Rick Anderson](https://twitter.com/RickAndMSFT) 고 [Luke Latham](https://github.com/guardrex)

웹 사이트는 자주 함께 작동 하는 개별 웹 앱의 구성 됩니다. 환경을 제공 하기 위해에서 single sign-on (SSO), 사이트 내에서 web apps 인증 쿠키를 공유 해야 합니다. 이런 시나리오에 대응하기 위해서, 데이터 보호 스택은 Katana 쿠키 인증 및 ASP.NET Core 쿠키 인증 티켓의 공유를 지원합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 샘플에서는 쿠키 인증을 사용 하는 세 가지 앱 간에 공유 되는 쿠키를 보여 줍니다.

* ASP.NET Core 2.0 Razor 페이지 앱을 사용 하지 않고 [ASP.NET Core Id](xref:security/authentication/identity)
* ASP.NET Core Id 사용 하 여 ASP.NET Core 2.0 MVC 앱
* ASP.NET Id를 사용 하 여 ASP.NET Framework 4.6.1 MVC 앱

다음에 나오는 예제:

* 인증 쿠키 이름은 일반적인 값으로 설정 됩니다 `.AspNet.SharedCookie`합니다.
* 합니다 `AuthenticationType` 로 설정 된 `Identity.Application` 명시적으로 나 기본적으로 합니다.
* 데이터 보호 키를 공유 하도록 데이터 보호 시스템을 사용 하도록 설정 하는 일반적인 앱 이름이 사용 됩니다 (`SharedCookieApp`).
* `Identity.Application` 인증 체계로 사용 됩니다. 어떤 방식이 사용 된, 일관 되 게 사용 해야 합니다 *내부와 여러* 기본 체계 또는 명시적으로 설정 하 여 공유 쿠키 앱. 스키마를 암호화 하 고 앱에서 일관 된 스키마를 사용 해야 하므로 쿠키를 암호 해독 하는 경우에 사용 됩니다.
* 일반적인 [데이터 보호 키](xref:security/data-protection/implementation/key-management) 저장소 위치가 사용 됩니다. 라는 폴더를 사용 하는 샘플 앱 *링* 데이터 보호 키를 저장할 솔루션의 루트에 있습니다.
* ASP.NET Core 앱에서 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 키 저장소 위치를 설정 하는 데 사용 됩니다. [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 일반적인 공유 앱 이름 구성 하는 데 사용 됩니다.
* .NET Framework 앱에서 쿠키 인증 미들웨어를 사용 하 여 구현의 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)합니다. `DataProtectionProvider` 암호화 및 인증 쿠키 페이로드 데이터의 암호 해독에 대 한 데이터 보호 서비스를 제공합니다. `DataProtectionProvider` 인스턴스는 앱의 다른 부분에서 사용 되는 데이터 보호 시스템에서 격리 됩니다.
  * [DataProtectionProvider.Create (System.IO.DirectoryInfo, 작업\<IDataProtectionBuilder >)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_System_Action_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder__) 허용 된 [DirectoryInfo](/dotnet/api/system.io.directoryinfo) 데이터 보호 키 저장소에 대 한 위치를 지정 합니다. 샘플 앱의 경로 제공 합니다 *인증 키* 폴더를 `DirectoryInfo`입니다. [DataProtectionBuilderExtensions.SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionBuilderExtensions_SetApplicationName_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_) 일반적인 앱 이름을 설정 합니다.
  * [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) 를 사용하려면 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet 패키지가 필요합니다. ASP.NET Core 2.1 이상 앱에이 패키지를 가져오려면 다음을 참조 합니다 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app)합니다. .NET Framework를 대상으로 하는 경우에 패키지 참조 추가 `Microsoft.AspNetCore.DataProtection.Extensions`합니다.

## <a name="share-authentication-cookies-among-aspnet-core-apps"></a>ASP.NET Core 앱 간에 인증 쿠키 공유

ASP.NET Core Id를 사용 하 여 하는 경우:

::: moniker range=">= aspnetcore-2.0"

에 `ConfigureServices` 메서드를 사용 하 여 합니다 [ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie) 확장 메서드를 쿠키에 대 한 데이터 보호 서비스 설정 합니다.

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

앱 이름과 데이터 보호 키는 앱 간에 공유 해야 합니다. 샘플 앱에서 `GetKeyRingDirInfo` 일반적인 키 저장 위치를 반환 합니다 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 메서드. 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 일반적인 공유 앱 이름을 구성 하려면 (`SharedCookieApp` 예제의). 자세한 내용은 [데이터 보호 구성](xref:security/data-protection/configuration/overview)합니다.

하위 도메인 간에 쿠키 공유 하는 앱을 호스팅하는 경우에 공용 도메인을 지정 합니다 [Cookie.Domain](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain) 속성입니다. 에 앱 간에 쿠키 공유를 `contoso.com`와 같은 `first_subdomain.contoso.com` 및 `second_subdomain.contoso.com`를 지정 합니다 `Cookie.Domain` 으로 `.contoso.com`:

```csharp
options.Cookie.Domain = ".contoso.com";
```

참조를 *CookieAuthWithIdentity.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).

::: moniker-end

::: moniker range="< aspnetcore-2.0"

에 `Configure` 메서드를 사용 하 여 합니다 [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions) 설정 하려면:

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

::: moniker-end

쿠키를 직접 사용 하는 경우:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]

앱 이름과 데이터 보호 키는 앱 간에 공유 해야 합니다. 샘플 앱에서 `GetKeyRingDirInfo` 일반적인 키 저장 위치를 반환 합니다 [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) 메서드. 사용 하 여 [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) 일반적인 공유 앱 이름을 구성 하려면 (`SharedCookieApp` 예제의). 자세한 내용은 [데이터 보호 구성](xref:security/data-protection/configuration/overview)합니다.

하위 도메인 간에 쿠키 공유 하는 앱을 호스팅하는 경우에 공용 도메인을 지정 합니다 [Cookie.Domain](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain) 속성입니다. 에 앱 간에 쿠키 공유를 `contoso.com`와 같은 `first_subdomain.contoso.com` 및 `second_subdomain.contoso.com`를 지정 합니다 `Cookie.Domain` 으로 `.contoso.com`:

```csharp
options.Cookie.Domain = ".contoso.com";
```

참조를 *CookieAuth.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).

::: moniker-end

::: moniker range="< aspnetcore-2.0"


```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
});
```

::: moniker-end

## <a name="encrypting-data-protection-keys-at-rest"></a>미사용 데이터 보호 키는 암호화

프로덕션 배포에 구성 된 `DataProtectionProvider` DPAPI 또는 X509Certificate를 사용 하 여 미사용 키를 암호화 하 합니다. 참조 [미사용 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest) 자세한 내용은 합니다.

::: moniker range=">= aspnetcore-2.0"

```csharp
services.AddDataProtection()
    .ProtectKeysWithCertificate("thumbprint");
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

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

::: moniker-end

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-apps"></a>ASP.NET 4.x 응용 프로그램과 ASP.NET Core 응용 프로그램 간 인증 쿠키 공유하기

Katana 쿠키 인증 미들웨어를 사용하는 ASP.NET 4.x 응용 프로그램은 ASP.NET Core 쿠키 인증 미들웨어와 호환되는 인증 쿠키를 생성하도록 구성할 수 있습니다. 이렇게 하면 사이트 전체에 걸쳐 원활한 SSO 경험을 제공 하는 동안 증분 대규모 사이트의 개별 앱을 업그레이드 합니다.

앱에서 Katana 쿠키 인증 미들웨어를 사용 하는 경우 호출 `UseCookieAuthentication` 프로젝트의 *Startup.Auth.cs* 파일입니다. ASP.NET 4.x 웹 앱 프로젝트는 Visual Studio 2013을 사용 하 여 만들어지고 나중 Katana 쿠키 인증 미들웨어를 사용 하 여 기본적으로. 하지만 `UseCookieAuthentication` 사용 되지 않으며를 호출 하는 ASP.NET Core 앱에 대 한 지원 되지 않는 `UseCookieAuthentication` Katana를 사용 하는 ASP.NET 4.x 앱 쿠키 인증 미들웨어의 유효 합니다.

ASP.NET 4.x 앱.NET Framework 4.5.1을 대상 해야 이상. 그렇지 않으면 필요한 NuGet 패키지를 설치 하지 못했습니다.

ASP.NET 4.x 앱 및 ASP.NET Core 앱 간에 인증 쿠키를 공유 하려면 위에서 설명한 것 처럼 ASP.NET Core 앱을 구성 하 고이 단계를 수행 하 여 ASP.NET 4.x 앱 구성:

1. 패키지를 설치 [Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/) 각 ASP.NET 4.x 응용 프로그램입니다.

2. *Startup.Auth.cs* 파일에서 `UseCookieAuthentication` 에 대한 호출을 찾고 다음과 같이 수정합니다. ASP.NET Core 쿠키 인증 미들웨어에서 사용 하는 이름에 일치 시키려면 쿠키 이름을 변경 합니다. 인스턴스를 제공 된 `DataProtectionProvider` 일반 데이터 보호 키 저장소 위치를 초기화 합니다. 앱 이름 쿠키를 공유 하는 모든 앱에서 사용 하는 일반적인 앱 이름으로 설정 되어 있는지 확인 `SharedCookieApp` 샘플 앱에서입니다.

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]

참조를 *CookieAuthWithIdentity.NETFramework* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).

인증 형식에 정의 된 형식과 일치 해야 사용자 id를 생성 하는 경우 `AuthenticationType` 집합과 `UseCookieAuthentication`합니다.

*Models/IdentityModels.cs*:

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]

## <a name="use-a-common-user-database"></a>일반적인 사용자 데이터베이스를 사용 합니다.

각 앱에 대 한 id 시스템이 동일한 사용자 데이터베이스에서 가리키고 있는지 확인 합니다. 이 고, 그렇지 id 시스템 데이터베이스의 정보에 대 한 인증 쿠키의 정보를 일치 시 키 려 고 하는 경우 런타임 시 오류를 생성 합니다.

## <a name="additional-resources"></a>추가 자료

<xref:host-and-deploy/web-farm>
