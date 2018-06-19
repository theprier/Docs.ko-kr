---
title: ClaimsPrincipal.Current에서 마이그레이션
author: mjrousos
description: 현재 인증 된 사용자의 id 및 ASP.NET 코어의 클레임을 검색 하는 ClaimsPrincipal.Current에서 마이그레이션하는 방법에 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/04/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/claimsprincipal-current
ms.openlocfilehash: ea43d17e76380baf57cd9debbc508e8812cfa4a6
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33851535"
---
# <a name="migrate-from-claimsprincipalcurrent"></a>ClaimsPrincipal.Current에서 마이그레이션

ASP.NET 프로젝트에서 사용 하는 것 [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) 현재 검색을 사용자의 id 및 클레임 인증입니다. ASP.NET Core에서 더 이상이 속성이 설정 되어 없습니다. 큰지에 된 코드를 다른 수단을 통해 현재 인증 된 사용자의 id를 가져오려면 업데이트 해야 합니다.

## <a name="context-specific-data-instead-of-static-data"></a>정적 데이터 대신 상황에 맞는 데이터

ASP.NET Core를 둘 다의 값을 사용 하는 경우 `ClaimsPrincipal.Current` 및 `Thread.CurrentPrincipal` 를 설정할 수 없습니다. 이러한 두 속성에는 ASP.NET Core 일반적으로 하지 않습니다. 정적 상태를 나타냅니다. ASP.NET Core 아키텍처 상황에 맞는 서비스 컬렉션에서 종속성 (예: 현재 사용자의 id)를 검색 하는 대신 (사용 하 여 해당 [종속성 주입](xref:fundamentals/dependency-injection) (DI) 모델). 더 이란 `Thread.CurrentPrincipal` 는 스레드 정적 이므로 비동기 일부 시나리오에서는 변경 내용이 유지 되지 않을 수 있습니다 (및 `ClaimsPrincipal.Current` 호출 `Thread.CurrentPrincipal` 기본적으로).

문제 스레드의 종류를 이해 하려면 정적 멤버 비동기 시나리오에서 다음 코드 조각을 참조 하십시오 발생할 수 있습니다.

```csharp
// Create a ClaimsPrincipal and set Thread.CurrentPrincipal
var identity = new ClaimsIdentity();
identity.AddClaim(new Claim(ClaimTypes.Name, "User1"));
Thread.CurrentPrincipal = new ClaimsPrincipal(identity);

// Check the current user
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");

// For the method to complete asynchronously
await Task.Yield();

// Check the current user after
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");
```

위의 샘플 코드 집합 `Thread.CurrentPrincipal` 비동기 호출을 대기 하기 전후에 해당 값을 확인 하 고 있습니다. `Thread.CurrentPrincipal` 관련는 *스레드* 기반이 설정 하 고 메서드가 await 뒤에 다른 스레드에서 실행을 다시 시작 될 수 있습니다. 따라서 `Thread.CurrentPrincipal` 은 present를 먼저 검사 하지만를 호출한 후 null 때 `await Task.Yield()`합니다.

응용 프로그램의 DI 서비스 컬렉션에서 현재 사용자의 id를 가져오는 없으므로 더 테스트 가능한도 테스트 identities 쉽게 삽입 될 수 있습니다.

## <a name="retrieve-the-current-user-in-an-aspnet-core-app"></a>ASP.NET Core 응용 프로그램에서 현재 사용자를 검색 합니다.

현재 인증 된 사용자를 검색 하기 위한 여러 가지 `ClaimsPrincipal` 대신 ASP.NET Core에서 `ClaimsPrincipal.Current`:

* **ControllerBase.User**합니다. MVC 컨트롤러와 현재 인증 된 사용자에 액세스할 수 있는 해당 [사용자](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) 속성입니다.
* **HttpContext.User**합니다. 현재에 액세스할 수 있는 구성 요소 `HttpContext` (예: 미들웨어) 현재 사용자를 가져올 수 `ClaimsPrincipal` 에서 [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)합니다.
* **호출자에서 전달 된**합니다. 현재에 액세스 하지 않고 라이브러리 `HttpContext` 컨트롤러 또는 미들웨어 구성 요소에서 통칭 되 고 인수로 전달 하는 현재 사용자의 id를 가질 수 있습니다.
* **IHttpContextAccessor**합니다. ASP.NET Core로 마이그레이션되는 ASP.NET 프로젝트는 필요한 모든 위치에 현재 사용자의 id를 쉽게 전달할 수 없을 정도로 수 있습니다. 이러한 경우 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 해결 방법으로 사용할 수 있습니다. `IHttpContextAccessor` 현재 액세스할 수 `HttpContext` (있는 경우). ASP.NET Core DI 기반 아키텍처와 함께 작동 하도록 아직 업데이트 되지 않은 코드에서 현재 사용자의 id를 가져오는 단계는 임시 솔루션이 합니다.

  * 확인 `IHttpContextAccessor` 호출 하 여 DI 컨테이너에서 사용할 수 있는 [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) 에서 `Startup.ConfigureServices`합니다.
  * 인스턴스를 가져올 `IHttpContextAccessor` 시작 하는 동안를 정적 변수에 저장 합니다. 인스턴스를 이전에 정적 속성에서 현재 사용자를 검색 하는 코드를 사용할 수 있습니다.
  * 현재 사용자의 검색 `ClaimsPrincipal` 를 사용 하 여 `HttpContextAccessor.HttpContext?.User`합니다. 이 코드는 HTTP 요청의 컨텍스트 외부에서 사용 되는 경우는 `HttpContext` null입니다.

최종 옵션을 사용 하 여 `IHttpContextAccessor`, ASP.NET Core 원칙 (정적 종속성에 삽입 된 종속성을 선호)에 위배 됩니다. 정적에 대 한 종속성을 제거할 계획 `IHttpContextAccessor` 도우미입니다. 것이 유용한 브리지 하지만 이전에 사용 하는 큰 기존 ASP.NET 응용 프로그램을 마이그레이션할 때 `ClaimsPrincipal.Current`합니다.
