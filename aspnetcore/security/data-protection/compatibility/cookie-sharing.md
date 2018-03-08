---
title: "응용 프로그램 간 쿠키 공유하기"
author: rick-anderson
description: "이 문서에서는 데이터 보호 스택이 ASP.NET 4.x 및 ASP.NET Core 응용 프로그램 간에 인증 쿠키 공유를 지원하는 방법을 알아봅니다."
keywords: "ASP.NET Core,ASP.NET,쿠키,Interop,쿠키 공유"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 9a7aae45-8e21-4c54-950c-3c29df6c1082
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/compatibility/cookie-sharing
ms.openlocfilehash: f026a287601a51e544482b95c5283e8ee960d656
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="sharing-cookies-between-applications"></a>응용 프로그램 간 쿠키 공유하기

일반적으로 웹 사이트는 서로 조화롭게 동작하는 다수의 개별적인 웹 응용 프로그램으로 구성되는 경우가 많습니다. 따라서 응용 프로그램 개발자가 훌륭한 Single Sign-On 경험을 제공하기 위해서는 사이트에 존재하는 모든 개별 웹 응용 프로그램들 간에 서로 인증 티켓을 공유해야 하는 경우가 종종 발생합니다.

이런 시나리오에 대응하기 위해서, 데이터 보호 스택은 Katana 쿠키 인증 및 ASP.NET Core 쿠키 인증 티켓의 공유를 지원합니다.

## <a name="sharing-authentication-cookies-between-applications"></a>응용 프로그램 간 인증 쿠키 공유하기

두 개의 다른 ASP.NET Core 응용 프로그램 간에 서로 인증 쿠키를 공유하려면, 쿠키를 공유할 응용 프로그램들을 각각 다음과 같이 구성합니다.

구성 메서드에서 `CookieAuthenticationOptions`를 이용해서 쿠키에 관련된 데이터 보호 서비스를 설정하고 `AuthenticationScheme`을 ASP.NET 4.X에 적합하게 설정합니다.
* 쿠키 인증 미들웨어의 구현을 사용 하 여 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)합니다. `DataProtectionProvider` 암호화 및 인증 쿠키 페이로드 데이터의 암호 해독에 대 한 데이터 보호 서비스를 제공합니다. `DataProtectionProvider` 인스턴스 응용 프로그램의 다른 부분에서 사용 되는 데이터 보호 시스템에서 격리 됩니다.
[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

Identity를 사용 중인 경우:

```csharp
app.AddIdentity<ApplicationUser, IdentityRole>(options =>
{
    options.Cookies.ApplicationCookie.AuthenticationScheme = "ApplicationCookie";
    var protectionProvider = DataProtectionProvider.Create(new DirectoryInfo(@"c:\shared-auth-ticket-keys\"));
    options.Cookies.ApplicationCookie.DataProtectionProvider = protectionProvider;
    options.Cookies.ApplicationCookie.TicketDataFormat = new TicketDataFormat(protectionProvider.CreateProtector("Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware", "Cookies", "v2"));
});
```

쿠키를 직접 사용할 경우:

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]
```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = DataProtectionProvider.Create(new DirectoryInfo(@"c:\shared-auth-ticket-keys\"))
});
```

`DataProtectionProvider`를 사용하려면 `Microsoft.AspNetCore.DataProtection.Extensions` NuGet 패키지가 필요합니다.

이 방식을 사용할 경우, `DirectoryInfo`는 인증 쿠키 전용으로 따로 준비된 키 저장소의 위치를 가리켜야 합니다. 쿠키 인증 미들웨어는 명시적으로 제공된 `DataProtectionProvider`의 구현을 사용하게 되며, 이로 인해서 응용 프로그램의 다른 영역에서 사용되는 데이터 보호 시스템과 격리됩니다. 이때, 응용 프로그램들 간의 격리를 위해서 삽입되는 응용 프로그램 이름은 무시됩니다 (이는 의도적인 것으로, 여러 응용 프로그램에서 페이로드를 공유하려고 시도하고 있기 때문입니다).

>[!WARNING]
>다음 예제처럼 `DataProtectionProvider`를 구성해서 저장된 비활성 키를 암호화하는 방안을 고려하시기 바랍니다.
>
>
>  ```csharp
>  app.UseCookieAuthentication(new CookieAuthenticationOptions
>  {
>      DataProtectionProvider = DataProtectionProvider.Create(
>          new DirectoryInfo(@"c:\shared-auth-ticket-keys\"),
>          configure =>
>          {
>              configure.ProtectKeysWithCertificate("thumbprint");
>          })
>  });
>  ```

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-applications"></a>ASP.NET 4.x 응용 프로그램과 ASP.NET Core 응용 프로그램 간 인증 쿠키 공유하기

Katana 쿠키 인증 미들웨어를 사용하는 ASP.NET 4.x 응용 프로그램은 ASP.NET Core 쿠키 인증 미들웨어와 호환되는 인증 쿠키를 생성하도록 구성할 수 있습니다. 이를 활용하면 대규모 사이트를 구성하는 각각의 응용 프로그램들을 단계적으로 업그레이드 하면서, 동시에 계속해서 사이트 전체에 걸친 원활한 Single Sign 경험을 제공할 수 있습니다.

>[!TIP]
> 프로젝트의 Startup.Auth.cs 파일에서 `UseCookieAuthentication`을 호출하는 코드가 존재하는지 확인해보면 기존 응용 프로그램이 Katana 쿠키 미들웨어를 사용하는지 여부를 알 수 있습니다. Visual Studio 2013 및 그 이후 버전에서 생성된 ASP.NET 4.x 웹 응용 프로그램은 기본적으로 Katana 쿠키 인증 미들웨어를 사용합니다.

> [!NOTE]
> ASP.NET 4.x 응용 프로그램은 .NET Framework 4.5.1 또는 그 이후 버전을 대상으로 해야 합니다. 그렇지 않으면 필수 NuGet 패키지가 설치되지 않습니다.

ASP.NET 4.x 응용 프로그램과 ASP.NET Core 응용 프로그램 간에 인증 쿠키를 공유하려면, 앞에서 설명한 것처럼 ASP.NET Core 응용 프로그램을 구성하고 다음과 같은 과정에 따라 ASP.NET 4.x 응용 프로그램을 구성합니다.

1.  `Microsoft.Owin.Security.Interop` 패키지를 대상 ASP.NET 4.x 응용 프로그램에 설치합니다.

2.  Startup.Auth.cs 파일에서 `UseCookieAuthentication`을 호출하는 코드를 찾습니다. 일반적으로 다음과 같은 형태를 갖고 있습니다.

    ```csharp
    app.UseCookieAuthentication(new CookieAuthenticationOptions
[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]
        // ...
    });
    ```
[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]
    
3.  다음과 같이 `UseCookieAuthentication` 호출을 수정해서, CookieName을 ASP.NET Core 쿠키 인증 미들웨어에서 사용되는 이름과 동일하게 변경하고, 키 저장소 경로를 전달해서 초기화 한 `DataProtectionProvider`의 인스턴스를 제공하고, 청크 형식이 호환되도록 `CookieManager`를 Interop `ChunkingCookieManager`로 설정합니다.

    ```csharp
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
        CookieName = ".AspNetCore.Cookies",
        // CookieName = ".AspNetCore.ApplicationCookie", (if you're using identity)
        // CookiePath = "...", (if necessary)
        // ...
        TicketDataFormat = new AspNetTicketDataFormat(
            new DataProtectorShim(
                DataProtectionProvider.Create(new DirectoryInfo(@"c:\shared-auth-ticket-keys\"))
                .CreateProtector("Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware",
                "Cookies", "v2"))),
        CookieManager = new ChunkingCookieManager()
    });
    ```
    `DirectoryInfo`는 ASP.NET Core 응용 프로그램에서 지정한 저장소 위치와 동일한 경로를 가리켜야 하고 동일한 설정을 사용해서 구성돼야 합니다.

이렇게 구성하면 ASP.NET 4.x 및 ASP.NET Core 응용 프로그램이 인증 쿠키를 공유하게 됩니다.

> [!NOTE]
> 각 응용 프로그램의 Identity 시스템이 동일한 사용자 데이터베이스를 바라보고 있는지 확인해야 합니다. 그렇지 않으면, 런타임 시에 Identity 시스템이 인증 쿠키의 정보와 데이터베이스의 정보가 일치하는지 여부를 확인할 때 오류가 발생합니다.
