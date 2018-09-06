---
title: ASP.NET Core에서 HTTPS 적용
author: rick-anderson
description: 웹 앱을 ASP.NET Core에서 HTTPS/TLS를 요구 하는 방법에 보여 줍니다.
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 838cd00545f36736461616f806942249aaf6eee0
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893180"
---
# <a name="enforce-https-in-aspnet-core"></a>ASP.NET Core에서 HTTPS 적용

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 다음과 같은 내용을 살펴봅니다.

* 모든 요청에 대 한 HTTPS가 필요 합니다.
* 모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.

API가 없습니다. 첫 번째 요청 시 중요 한 데이터를 보낸 클라이언트를 방지할 수 있습니다.

> [!WARNING]
> 수행할 **되지** 사용 하 여 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 중요 한 정보를 수신 하는 Web Api에서 합니다. `RequireHttpsAttribute` 브라우저는 HTTP에서 HTTPS로 리디렉션하 HTTP 상태 코드를 사용 합니다. API 클라이언트 이해 하지 못하거나 HTTP에서 HTTPS로 리디렉션 준수 될 수 있습니다. 이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다. Web Api을 수행 해야합니다.
>
> * HTTP에서 수신 대기할 수 없습니다.
> * 상태 코드 400 (잘못 된 요청)를 사용 하 여 연결을 닫고 요청을 제공 하지 마십시오.

<a name="require"></a>
## <a name="require-https"></a>HTTPS가 필요

::: moniker range=">= aspnetcore-2.1"

모든 프로덕션 ASP.NET Core 웹 앱 호출을 좋습니다.

* HTTPS 리디렉션을 미들웨어 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) HTTPS로 모든 HTTP 요청을 리디렉션할 수 있습니다.
* [UseHsts](#hsts), HTTP 엄격한 전송 보안 (HSTS) 프로토콜입니다.

### <a name="usehttpsredirection"></a>UseHttpsRedirection

다음 코드 호출 `UseHttpsRedirection` 에 `Startup` 클래스:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

위의 강조 표시 된 코드:

* 기본값을 사용 하 여 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).
* 기본값을 사용 하 여 [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) 의해 재정의 되지 않는 (null)은 `ASPNETCORE_HTTPS_PORT` 환경 변수 또는 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)합니다.

> [!WARNING] 
>포트를 HTTPS로 리디렉션하는 미들웨어에 대 한 사용할 수 있어야 합니다. 사용 가능한 포트가 없는 경우 HTTPS로 리디렉션 발생 하지 않습니다. 다음 설정 중 하나에서 HTTPS 포트를 지정할 수 있습니다.
> 
>* `HttpsRedirectionOptions.HttpsPort` 
>* `ASPNETCORE_HTTPS_PORT` 환경 변수입니다. 
>* HTTPS url 사용 하 여 개발에서 *launchsettings.json*합니다. 
>* Kestrel 또는 HttpSys에 직접 구성 하는 HTTPS url입니다. 

다음 코드 호출을 강조 표시 [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) 미들웨어 옵션을 구성 하려면:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

호출 `AddHttpsRedirection` 값을 변경 하는 데 필요한 전용인 ` HttpsPort` 또는 ` RedirectStatusCode`;

위의 강조 표시 된 코드:

* 집합 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) 에 `Status307TemporaryRedirect`, 기본 값입니다.
* HTTPS 포트를 5001로 설정합니다. 기본값은 443입니다.

다음과 같은 메커니즘 포트를 자동으로 설정 합니다.

* 미들웨어를 통해 포트를 검색할 수 있습니다 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) 다음 조건이 적용 되는 경우:

   * Kestrel 또는 HTTPS 끝점으로 직접 사용 됩니다 (Visual Studio Code의 디버거를 사용 하 여 앱을 실행 하도 적용 됨).
   * 만 **하나의 HTTPS 포트** 앱에서 사용 됩니다.

* Visual Studio는 사용 합니다.
   * IIS Express에 HTTPS를 사용 해야 합니다.
   * *launchSettings.json* 설정의 `sslPort` IIS Express에 대 한 합니다.

> [!NOTE]
> 앱 (예를 들어, IIS, IIS Express) 역방향 프록시 뒤에 실행 될 때 `IServerAddressesFeature` 사용할 수 없습니다. 포트를 수동으로 구성 해야 합니다. 포트 설정 되지 않은 경우 요청을 리디렉션할 되지 않습니다.

설정 하 여 포트를 구성할 수 있습니다 합니다 [https_port 웹 호스트 구성 설정을](xref:fundamentals/host/web-host#https-port):

**키**: https_port  
**형식**: *string*  
**기본**: 기본값이 설정 되지 않습니다.  
**설정 방법**: `UseSetting`  
**환경 변수**: `<PREFIX_>HTTPS_PORT` (접두사는 `ASPNETCORE_` 웹 호스트를 사용 하는 경우입니다.)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> URL을 설정 하 여 포트를 직접 구성할 수 있습니다는 `ASPNETCORE_URLS` 환경 변수입니다. 환경 변수를 구성 서버에을 수행한 후 미들웨어 직접 검색 되지 HTTPS 포트를 통해 `IServerAddressesFeature`합니다.

경우 포트가 없는 설정 됩니다.

* 요청을 리디렉션할 되지 않습니다.
* 미들웨어 "리디렉션에 대 한 https 포트를 확인 하지 못했습니다." 경고를 기록 합니다.

> [!NOTE]
> HTTPS 리디렉션을 미들웨어를 사용 하는 대신 (`UseHttpsRedirection`) URL 재작성 미들웨어를 사용 하는 것 (`AddRedirectToHttps`). `AddRedirectToHttps` 리디렉션 실행 될 때 상태 코드 및 포트를 설정할 수도 있습니다. 자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다.
>
> 추가 리디렉션 규칙을 요구 하지 않고 HTTPS로 리디렉션, 하는 경우 HTTPS 리디렉션을 미들웨어를 사용 하는 것이 좋습니다 (`UseHttpsRedirection`)이이 항목에서 설명 합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.1"

합니다 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) HTTPS가 필요 하는 데 사용 됩니다. `[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전체적으로 적용할 수 있습니다. 특성을 전역적으로 적용 하려면 다음 코드를 추가 합니다 `ConfigureServices` 에서 `Startup`:

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다. 다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다. 또한 미들웨어 리디렉션 실행 될 때 상태 코드 또는 상태 코드와 포트를 설정 하려면 앱을 허용 합니다.

전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`). 적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성에 전역적으로 HTTPS를 요구 하는 것 만큼 안전로 간주 되지 않습니다. 보장할 수 없습니다는 `[RequireHttps]` 새 컨트롤러 및 Razor 페이지는 추가 특성이 적용 됩니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a>HTTP 엄격한 전송 보안 프로토콜 (HSTS)

당 [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)하십시오 [HTTP 엄격한 전송 보안 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 응답 헤더를 사용 하 여 웹 앱에서 지정 하는 옵트인 보안 향상 된 기능입니다. 경우는 [HSTS를 지 원하는 브라우저](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support) 이 헤더를 수신 합니다.

* 브라우저에는 모든 통신이 HTTP를 통해 보낼 수 없는 도메인에 대 한 구성을 저장 합니다. 브라우저 강제로 HTTPS를 통해 모든 통신을 수행합니다.
* 브라우저에서 신뢰할 수 없거나 잘못 된 인증서를 사용 하 여 사용자를 방지 합니다. 브라우저 사용자가 일시적으로 이러한 인증서를 신뢰 하는 프롬프트를 비활성화 합니다.

HSTS는 클라이언트에서 적용 하기 때문에 몇 가지 제한 사항이 있습니다.

* 클라이언트는 HSTS를 지원 해야 합니다.
* HSTS는 HSTS 정책을 설정 하려면 하나 이상의 성공적인 HTTPS 요청에 필요 합니다.
* 응용 프로그램이 모든 HTTP 요청을 확인 하 고 리디렉션 하거나 HTTP 요청을 거부 해야 합니다.

ASP.NET Core 2.1 이상을 사용 하 여 HSTS를 구현 합니다 `UseHsts` 확장 메서드. 다음 코드 호출 `UseHsts` 에 앱이 없는 경우 [개발 모드](xref:fundamentals/environments):

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

`UseHsts` 권장 되지 않습니다 개발에서 HSTS 설정이 항상 캐시할 수 있기 때문에 브라우저에서. 기본적으로 `UseHsts` 로컬 루프백 주소를 제외 합니다.

처음에 대 한 HTTPS를 구현 하는 프로덕션 환경에서는 초기 HSTS 값을 작은 값으로 설정 합니다. 값을 설정할 시간에서 전혀 보다 하루를 HTTP로 HTTPS 인프라를 되돌려야 하는 경우. HTTPS 구성의 유지 가능성에 확신한 후 늘릴 HSTS 최대 처리 기간 값 자주 사용 되는 값은 1 년입니다. 

다음 예를 참조하십시오.

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* Strict-전송-보안 헤더의 미리 로드 매개 변수를 설정합니다. Preload의 일부가 아닌 합니다 [RFC HSTS 사양](https://tools.ietf.org/html/rfc6797), 있지만 HSTS 새로 설치할 때 사이트를 미리 로드 하려면 웹 브라우저에서 지원 됩니다. 자세한 내용은 [https://hstspreload.org/](https://hstspreload.org/)를 참조하세요.
* 사용 하도록 설정 [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), 호스트 하위 도메인에 HSTS 정책을 적용 합니다. 
* 60 일로 Strict-전송-보안 헤더의 최대 처리 기간 매개 변수를 명시적으로 설정합니다. 설정 하지 않으면 기본값은 30 일입니다. 참조 된 [최대 처리 기간 지시문](https://tools.ietf.org/html/rfc6797#section-6.1.1) 자세한 내용은 합니다.
* 추가 `example.com` 를 제외 하는 호스트의 목록입니다.

`UseHsts` 다음 루프백 호스트를 제외:

* `localhost` : IPv4 루프백 주소입니다.
* `127.0.0.1` : IPv4 루프백 주소입니다.
* `[::1]` : IPv6 루프백 주소입니다.

앞의 예제에는 추가 호스트를 추가 하는 방법을 보여 줍니다.
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a>옵트아웃 https 프로젝트 생성 시

ASP.NET Core 2.1 이상 웹 응용 프로그램 템플릿 (Visual Studio 또는 dotnet 명령 줄)에서 사용 하도록 설정 [HTTPS 간의 리디렉션으로](#require) 하 고 [HSTS](#hsts)합니다. HTTPS를 요구 하지 않는 배포에 대 한 있습니다 옵트아웃할 수 https입니다. 예를 들어, 일부 백 엔드 서비스는 HTTPS 처리 되 고 외부 가장자리에 HTTPS를 사용 하 여 각 노드에서 필요 하지 않습니다.

옵트아웃 하려면 https:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

선택 취소 합니다 **HTTPS에 대 한 구성** 확인란을 선택 합니다.

![엔터티 다이어그램](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

`--no-https` 옵션을 사용합니다. 예

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-set-up-a-developer-certificate-for-docker"></a>Docker에 대 한 개발자 인증서를 설정 하는 방법

참조 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6199)합니다.

::: moniker-end

## <a name="additional-information"></a>추가 정보

* [OWASP HSTS 브라우저 지원](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)
