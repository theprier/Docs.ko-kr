---
title: ASP.NET Core에 HTTPS를 적용 합니다.
author: rick-anderson
description: 웹 응용 프로그램에서 ASP.NET Core HTTPS/TLS를 요청 하는 방법을 보여 줍니다.
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: 24ab83192ded381b46fab337a986f51fb22b2227
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729502"
---
# <a name="enforce-https-in-aspnet-core"></a>ASP.NET Core에 HTTPS를 적용 합니다.

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 문서에서는 다음과 같은 내용을 살펴봅니다.

* 모든 요청에 대 한 HTTPS가 필요 합니다.
* 모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.

> [!WARNING]
> 수행 **하지** 사용 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 중요 한 정보를 수신 하는 웹 Api에 있습니다. `RequireHttpsAttribute` HTTP 상태 코드를 사용 하 여 HTTP에서 HTTPS로 브라우저를 리디렉션합니다. API 클라이언트 이해 하지 못하거나 리디렉션을 HTTP에서 HTTPS로 준수 수 있습니다. 이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다. 웹 Api 하거나 수행 해야합니다.
>
> * HTTP에서 수신 하지 않습니다.
> * 상태 코드 400 (잘못 된 요청)와 연결을 닫고 요청을 처리 하지 마십시오.

<a name="require"></a>
## <a name="require-https"></a>HTTPS가 필요

::: moniker range=">= aspnetcore-2.1"

모든 ASP.NET Core 웹 앱 HTTPS 리디렉션 미들웨어를 호출 하는 것이 좋습니다 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection))를 HTTPS로 모든 HTTP 요청을 리디렉션합니다.

다음 호출 코드 `UseHttpsRedirection` 에 `Startup` 클래스:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

다음 호출 코드 [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) 미들웨어 옵션을 구성 하려면:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

앞의 강조 표시 된 코드:

* 집합 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)합니다.
* 5001를 HTTPS 포트를 설정합니다.

다음과 같은 메커니즘 포트를 자동으로 설정합니다.

* 미들웨어를 통해 포트를 검색할 수 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) 다음과 같은 조건이 적용 되는 경우:
  - Kestrel 또는 HTTP.sys HTTPS 끝점과 직접 사용 됩니다 (Visual Studio 코드의 디버거를 사용 응용 프로그램을 실행에 적용 됩니다).
  - 만 **하나의 HTTPS 포트** 응용 프로그램에서 사용 됩니다.
* Visual Studio는 사용 합니다.
  - IIS Express에 HTTPS를 사용할 수 있습니다.
  - *launchSettings.json* 설정의 `sslPort` IIS Express에 대 한 합니다.

> [!NOTE]
> 응용 프로그램 (예를 들어, IIS, IIS Express) 역방향 프록시 뒤에 실행 될 때 `IServerAddressesFeature` 사용할 수 없습니다. 포트가 수동으로 구성 되어야 합니다. 포트 설정 되지 않은 경우에 요청을 리디렉션할 되지 않습니다.

설정 하 여 포트를 구성할 수는 있습니다.

* `ASPNETCORE_HTTPS_PORT` 환경 변수.
* `http_port` 호스트 구성 키 (예를 들어 통해 *hostsettings.json* 또는 명령줄 인수).
* [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)합니다. 포트 5001를 설정 하는 방법을 보여 주는 앞의 예제를 참조 하십시오.

> [!NOTE]
> URL로 설정 하 여 포트를 직접 구성할 수 있습니다는 `ASPNETCORE_URLS` 환경 변수입니다. 환경 변수는 서버를 구성 및 다음 미들웨어 직접 검색 되지 HTTPS 포트를 통해 `IServerAddressesFeature`합니다.

포트가 없는 설정 되어 있습니다.

* 요청을 리디렉션할 되지 않습니다.
* 미들웨어는 경고를 기록 합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.1"

[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) HTTPS가 필요 하는 데 사용 됩니다. `[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전역으로 적용 될 수 있습니다. 특성을 전역으로 적용 하려면 다음 코드를 추가 `ConfigureServices` 에 `Startup`:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다. 다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

자세한 내용은 참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.

전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`). 적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다. 보장할 수는 `[RequireHttps]` 특성은 새 컨트롤러 및 Razor 페이지 추가 될 때 적용 됩니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a>HTTP 엄격한 전송 보안 프로토콜 (HSTS)

당 [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP 엄격한 전송 보안 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 는 특별 한 응답 헤더를 사용 하 여 웹 응용 프로그램에 의해 지정 된 옵트인 보안 향상 합니다. 지원 되는 브라우저는이 헤더를 수신 되 면 해당 브라우저의 통신을 지정한 도메인에 HTTP를 통해 보낼 수 없게 됩니다 및 HTTPS를 통해 모든 통신 송신할 대신 합니다. 또한 브라우저에 대 한 프롬프트를 통해 HTTPS 클릭을 수 없습니다.

ASP.NET Core 2.1 이상 HSTS와 구현 하는 `UseHsts` 확장 메서드. 다음 호출 코드 `UseHsts` 앱에 없는 경우 [개발 모드](xref:fundamentals/environments):

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

`UseHsts` 않으므로 개발에 권장 되는 HSTS 헤더는 항상 브라우저에서 캐시할. 기본적으로 UseHsts 로컬 루프백 주소를 제외합니다.

다음 예를 참조하십시오.

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* Strict-전송-보안 헤더의 미리 로드 매개 변수를 설정 합니다. 미리 로드를가의 일부가 [RFC HSTS 사양](https://tools.ietf.org/html/rfc6797), 있지만 HSTS 사이트 설치에 미리 로드 하려면 웹 브라우저에서 지원 됩니다. 자세한 내용은 [https://hstspreload.org/](https://hstspreload.org/)를 참조하세요.
* 수 있도록 [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), 하위 도메인의 호스트에 HSTS 정책을 적용 합니다. 
* 60 일 Strict-전송-보안 헤더의 최대 처리 기간 매개 변수를 명시적으로 설정합니다. 그렇지 않은 경우 30 일에 기본값을 설정 합니다. 참조는 [최대 처리 기간 지시문](https://tools.ietf.org/html/rfc6797#section-6.1.1) 자세한 정보에 대 한 합니다.
* 추가 `example.com` 제외 하는 호스트의 목록에 있습니다.

`UseHsts` 다음과 같은 루프백 호스트는 제외 됩니다.

* `localhost` : IPv4 루프백 주소입니다.
* `127.0.0.1` : IPv4 루프백 주소입니다.
* `[::1]` : IPv6 루프백 주소입니다.

앞의 예제에는 추가 호스트를 추가 하는 방법을 보여 줍니다.
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a>옵트아웃 HTTPS의 프로젝트 생성 시

(Visual Studio 또는 dotnet 명령줄)에서 ASP.NET Core 2.1 이상 웹 응용 프로그램 템플릿을 사용 [HTTPS 리디렉션](#require) 및 [HSTS](#hsts)합니다. HTTPS를 필요로 하지 않는 배포의 경우 있습니다 수 옵트아웃 https입니다. 예를 들어 일부 백 엔드 서비스에 HTTPS 처리 되 고 외부에서 경계 면 HTTPS를 사용 하 여 각 노드에서 필요 하지 않습니다.

되지 않게 하려면 https:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

취소는 **HTTPS에 대 한 구성** 확인란을 선택 합니다.

![엔터티 다이어그램](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

`--no-https` 옵션을 사용합니다. 예

```console
dotnet new webapp --no-https
```

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a>Docker에 대 한 개발자 인증서를 설치 하는 방법

참조 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6199)합니다.

::: moniker-end
