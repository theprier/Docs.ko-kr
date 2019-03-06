---
title: ASP.NET Core의 단일 페이지 응용 프로그램에 대 한 인증 소개
author: ''
description: ASP.NET Core 앱 내에서 호스팅되는 단일 페이지 응용 프로그램을 사용 하 여 Id를 사용 합니다.
ms.author: ''
ms.date: 03/05/2018
uid: security/authentication/identity/spa
ms.openlocfilehash: cf04ec1ff0ae9afea066fd1864ab0a7956ace32c
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57346786"
---
# <a name="authentication-and-authorization-for-spas"></a>인증 및 Spa에 대 한 권한 부여

ASP.NET 3.0에는 API 권한 부여에 대 한 새로운 지원을 통해,를 사용 하 여 단일 페이지 응용 프로그램의 인증에 대 한 지원이 도입 되었습니다. 이 지원 됩니다 인증 하 고 Open ID Connect 구현에 대 한 사용자 및 Id 서버 저장 ASP.NET Core Id의 조합의 기반으로 합니다.

새 인증 매개 변수는 Angular에 추가 했습니다 및 React 템플릿은 인증 매개 변수는 mvc 및 razor 페이지 템플릿 사용 하 여 유사한 허용 값 'None' 및 '개별'.

## <a name="create-an-angular-app-with-api-authorization-support"></a>API 권한 부여 지원을 통해 Angular 앱 만들기

인증 및 사용자의 권한 부여를 지 원하는 새 Angular 앱을 만들려면 명령 셸을 열고 다음 명령을 실행 합니다.

```console
dotnet new angular -o <output_directory_name> -au Individual
```

앞의 명령을 사용 하 여 ASP.NET Core 앱을 만듭니다는 *ClientApp* Angular 앱이 포함 된 디렉터리입니다.

## <a name="create-a-react-app-with-api-authorization-support"></a>API 권한 부여 지원을 통해 React 앱 만들기

인증 및 사용자의 권한 부여를 지 원하는 새 React 앱을 만들려면 명령 셸을 열고 다음 명령을 실행 합니다.

```console
dotnet new react -o <output_directory_name> -au Individual
```

앞의 명령을 사용 하 여 ASP.NET Core 앱을 만듭니다는 *ClientApp* React 앱이 포함 된 디렉터리입니다.

## <a name="general-description-of-the-aspnet-core-components-of-the-app"></a>앱의 ASP.NET Core 구성 요소에 대 한 일반적인 설명

인증에 대 한 지원을 포함 하는 경우 프로젝트에 대 한 몇 가지 추가 가지 있습니다.

### <a name="startup-class"></a>Startup 클래스

아래 Startup 클래스의 코드를 살펴보면 다음 포함 드립니다 수 있습니다.
* 내부 `public void ConfigureServices(IServiceCollection services)`:
  * 기본 UI 사용 하 여 id입니다.
    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
      options.UseSqlite(Configuration.GetConnectionString("DefaultConnection")));

    services.AddDefaultIdentity<ApplicationUser>()
      .AddDefaultUI(UIFramework.Bootstrap4)
      .AddEntityFrameworkStores<ApplicationDbContext>();
    ```
  * Identity Server 추가 AddApiAuthorization 도우미 메서드를 사용 하 여 해당 설정 일부 기본 Identity Server를 기반으로 ASP.NET 규칙입니다.
    ```csharp
    services.AddIdentityServer()
      .AddApiAuthorization<ApplicationUser, ApplicationDbContext>();
    ```
  * Identity Server에서 생성 된 Jwt 토큰의 유효성을 검사 하도록 응용 프로그램을 구성 하는 추가 AddIdentityServerJwt 도우미 메서드를 사용 하 여 인증 합니다. 
    ```csharp
    services.AddAuthentication()
      .AddIdentityServerJwt();
    ```
* 내부 `public void Configure(IApplicationBuilder app)`:
  * 들어오는 요청에 자격 증명의 유효성을 검사 하 고 사용자 요청 컨텍스트를 설정 하는 일을 담당 하는 인증 미들웨어입니다.
    ```csharp
    app.UseAuthentication();
    ```
  * Open ID Connect 끝점을 노출 하는 identity server 미들웨어입니다.
    ```csharp
    app.UseIdentityServer();
    ```

### <a name="addapiauthorization"></a>AddApiAuthorization 
이 도우미 메서드는 지원 되는 구성을 사용 하려면 Id 서버를 구성 합니다. Identity Server 응용 프로그램 보안 문제를 처리 하기 위한 매우 강력 하 고 확장 가능한 프레임 워크 이지만 가장 일반적인 시나리오에 대해 알아야 할 필요 하지 않은 복잡성을 많이 노출 하는 동시에에 따라서 선택 규칙 집합 및 생각 하는 구성 옵션 좋은 시작 지점이 됩니다. 인증 요구 사항이 변경 되 면 필요에 맞게 사용자 지정할 수 있습니다 Identity Server의 모든 기능을 여전히 표시 됩니다.

### <a name="addidentityserverjwt"></a>AddIdentityServerJwt
이 도우미 메서드는 기본 인증 처리기로 응용 프로그램에 대 한 정책 구성표를 구성합니다. Identity Id url 공간에 모든 하위 경로로 이동 하는 모든 요청을 처리할 수 있도록 정책이 구성 되어 "/ Identity" 및 다른 모든 요청을 처리 JwtBearerHandler 수 있도록 합니다.
Addionally이이 메서드는 등록을 `<<ApplicationName>>API` 의 기본 범위를 사용 하 여 id 서버를 사용 하 여 Api 리소스 `<<ApplicationName>>API` 하 고 응용 프로그램에 대 한 Identity Server에서 발급 된 토큰의 유효성을 검사 하 여 JWT 전달자 토큰 미들웨어를 구성 합니다.

### <a name="sampledatacontroller"></a>SampleDataController
Controllers\SampleDataController.cs 파일에 살펴봅니다 것을 볼 수 있습니다는 `[Authorize]` 리소스에 액세스 하는 기본 정책을 기반으로 사용자 권한을 부여 해야 함을 나타내는 클래스에 적용 된 특성입니다. 기본 권한 부여 정책을 통해 설정 되는 기본 인증 체계를 사용 하도록 구성 되어야 발생 `AddIdentityServerJwt` 위에서 설명한 정책 구성표를 하 여 JwtBearer 처리기 구성 이러한 도우미 메서드에서 대 한 기본 처리기 앱에 요청 합니다.

### <a name="applicationdbcontext"></a>ApplicationDbContext
Data\ApplicationDbContext.cs에서 파일을 보면 알 수 있습니다 ApiAuthorizationDbContext (IdentityDbContext에서 더 많이 파생 된 클래스)를 확장 하는 예외를 사용 하 여 id에 사용 된 동일한 DbContext Identity Server에 대 한 스키마를 포함 합니다.
데이터베이스 스키마의 전체 제어 하려는 경우에서는 간단히 사용할 수 있는 Identity DbContext 클래스 중 하나에서 상속 하 고 구성할 수를 호출 하 여 id 스키마를 포함 하는 상황에 맞는 `builder.ConfigurePersistedGrantContext(_operationalStoreOptions.Value)` 에 `OnModelCreating` 메서드.

### <a name="oidcconfigurationcontroller"></a>OidcConfigurationController
보면 파일 끝점을 보면 Controllers\OidcConfigurationController.cs OIDC 매개 변수를 사용 해야 하는 클라이언트에 맞도록 기립 했습니다.

### <a name="appsettingsjson"></a>appsettings.json
프로젝트의 루트에서 appsettings.json 파일을 보면 확인할 수 있습니다 새 `IdentityServer` 섹션 목록을 설명 하는 클라이언트를 구성 하 고 단일 클라이언트 인지 확인할 수 있습니다. 클라이언트의 응용 프로그램의 이름에 해당 이름과 oAuth ClientId 매개 변수 규칙으로 매핑됩니다. 프로필을 구성 하는 응용 프로그램의 유형을 나타냅니다 및 서버에 대 한 구성 프로세스를 간소화 하는 드라이브 규칙을 내부적으로 사용 합니다. 몇 가지 사용 가능한 프로필 아래 섹션에 설명 되어 있습니다.

```json
"IdentityServer": {
  "Clients": {
    "angularindividualpreview3final": {
      "Profile": "IdentityServerSPA"
    }
  }
}
```

### <a name="appsettingsdevelopmentjson"></a>appsettings.Development.json
Appsettings 보면. Development.json 파일 프로젝트의 루트를 보면 새 `IdentityServer` 토큰에 서명 하는 키를 설명 하는 섹션입니다. 프로덕션에 배포 하는 경우 키를 프로 비전 하 고 아래 설명 된 대로 응용 프로그램과 함께 배포 해야 합니다.

```json
  "IdentityServer": {
    "Key": {
      "Type": "Development"
    }
  }
}
```

## <a name="general-description-of-the-angular-application"></a>Angular 응용 프로그램에 대 한 일반적인 설명
Angular 모듈 자체에 거주 하는 인증 및 Angular 템플릿은 API 권한 부여에 대 한 지원. ClientApp\src\api에 대 한 권한 부여 및 것 같습니다. 다음과 같은 요소로 구성
* 구성 요소 3:
  * 로그인 구성 요소입니다. 앱에 대 한 로그인 흐름을 처리합니다.
  * 로그 아웃 구성 요소입니다. 앱에 대 한 로그 아웃 흐름을 처리합니다.
  * 로그인 메뉴 구성 요소: 현재 표시 된 위젯을 사용자 프로필을 관리 하 고 로그 아웃 링크를 사용 하 여 사용자를 인증 하거나 사용자가 인증 되지 않은 경우 등록 또는 로그인에 연결 합니다.
* 경로 가드 `AuthorizeGuard` 경로에 추가할 수 있습니다 하 고 사용자 경로 방문 하기 전에 인증 해야 합니다.
* Http 인터셉터 `AuthorizeInterceptor` 사용자가 인증 하는 경우에 API를 대상으로 나가는 HTTP 요청에 액세스 토큰을 연결 하는 합니다.
* 서비스 `AuthorizeService` 인증 프로세스의 더 낮은 수준의 세부 정보를 처리 하 고 소비 응용 프로그램의 나머지 부분에 인증된 된 사용자에 대 한 정보를 노출 합니다.
* 응용 프로그램의 인증 부분을 사용 하 여 연결 된 경로 정의 하 고 로그인 메뉴 구성 요소, 인터셉터, 가드 및 응용 프로그램의 나머지 부분에서 사용 하기 위해 서비스를 노출 하는 angular 모듈입니다.

## <a name="general-description-of-the-react-application"></a>React 응용 프로그램에 대 한 일반적인 설명
인증 및 React 템플릿은 생활 ClientApp\src\components\api authorization\ 하며 아래 API 권한 부여에 대 한 지원이 다음과 같은 요소로 구성 됩니다.
* 4 개 구성 요소가 있습니다.
  * 로그인 구성 요소입니다. 앱에 대 한 로그인 흐름을 처리합니다.
  * 로그 아웃 구성 요소입니다. 앱에 대 한 로그 아웃 흐름을 처리합니다.
  * 로그인 메뉴 구성 요소: 현재 표시 된 위젯을 사용자 프로필을 관리 하 고 로그 아웃 링크를 사용 하 여 사용자를 인증 하거나 사용자가 인증 되지 않은 경우 등록 또는 로그인에 연결 합니다.
  * AuthorizeRoute: 사용자 구성 요소 매개 변수에 지정 된 구성 요소를 렌더링 하기 전에 인증을 요구 하는 경로 구성 요소입니다.
  * 내보낸 `authService` 클래스의 인스턴스 `AuthorizeService` 인증 프로세스의 더 낮은 수준의 세부 정보를 처리 하 고 소비 응용 프로그램의 나머지 부분에 인증된 된 사용자에 대 한 정보를 노출 합니다.

솔루션의 주요 구성 요소에서 살펴본 했으므로 응용 프로그램에 대 한 개별 시나리오에서 특정 모양으로 취할 수 있습니다.

## <a name="requiring-authorization-on-a-new-api"></a>새 API에 필요한 권한 부여
시스템은 새 Api에 대 한 권한 부여를 요구 하도록 trivial 되도록 기본적으로 구성 됩니다. 이렇게 하려면 단순히 새 컨트롤러를 만들고 추가 `[Authorize]` 특성을 컨트롤러 클래스 또는 컨트롤러 내의 작업 합니다.

## <a name="protecting-a-client-side-route-angular"></a>클라이언트 쪽 경로 (Angular) 보호
클라이언트 쪽 경로 보호는 권한 부여 보호에 경로 구성 하는 경우를 실행 하는 가드의 목록에 추가 하 여 수행 됩니다. 예를 들어 기본 앱 angular 모듈 내에서 데이터를 가져오고 경로 구성 하는 방법을 확인할 수 있습니다.

```ts
RouterModule.forRoot([
  // ...
  { path: 'fetch-data', component: FetchDataComponent, canActivate: [AuthorizeGuard] },
])
```

경로 보호 합니다. 실제 끝점을 보호 하지 않습니다 언급 해야 (여전히 필요는 `[Authorize]` 특성이 적용) 있지만 해당만 사용자가 인증 되지 않은 경우 지정 된 클라이언트 쪽 경로 탐색에서 되지 않습니다.

## <a name="authenticate-api-requests-angular"></a>API 요청 (Angular) 인증

응용 프로그램은 HTTP 클라이언트 응용 프로그램에서 정의 된 인터셉터를 사용 하 여 자동으로 수행 됩니다 함께 호스트 되는 Api에 요청을 인증 합니다.

## <a name="protect-a-client-side-route-react"></a>클라이언트 쪽 경로 (React) 보호

클라이언트 쪽 경로 보호 하는 일반 경로 구성 요소 대신 AuthorizeRoute 구성 요소를 사용 하 여 수행 됩니다. 예를 들어 앱 구성 요소 내에서 데이터를 가져오고 경로 구성 하는 방법을 확인할 수 있습니다.

```jsx
<AuthorizeRoute path='/fetch-data' component={FetchData} />
```

경로 보호 합니다. 실제 끝점을 보호 하지 않습니다 언급 해야 (여전히 필요는 `[Authorize]` 특성이 적용) 있지만 해당만 사용자가 인증 되지 않은 경우 지정 된 클라이언트 쪽 경로 탐색에서 되지 않습니다.

## <a name="authenticate-api-requests-react"></a>API 요청 (React) 인증

먼저 이루어집니다 react 사용 하 여 요청을 인증 합니다 `authService` 에서 인스턴스는 `AuthorizeService` 는 authService에서 액세스 토큰을 검색 하 고 아래와 같이 요청에 연결 합니다. React 구성 요소에서 일반적으로 이렇게 componentDidMount 수명 주기 메서드 또는 결과에서 일부 사용자 상호 작용 합니다.

### <a name="import-the-authservice-into-your-component"></a>구성 요소에는 authService 가져오기

```js
import authService from './api-authorization/AuthorizeService'
```

### <a name="retrieve-and-attach-the-access-token-to-the-response"></a>검색 및 액세스 토큰 응답에 연결

```js
async populateWeatherData() {
  const token = await authService.getAccessToken();
  const response = await fetch('api/SampleData/WeatherForecasts', {
    headers: !token ? {} : { 'Authorization': `Bearer ${token}` }
  });
  const data = await response.json();
  this.setState({ forecasts: data, loading: false });
}
```

## <a name="deploy-into-production"></a>프로덕션 환경에 배포

프로덕션 환경에 응용 프로그램을 배포 하기 위해 몇 가지 리소스를 프로 비전 해야 합니다.
* Identity 사용자 계정 및 id 서버를 저장할 데이터베이스를 부여 합니다.
* 프로덕션 인증서를 토큰 서명에 사용 합니다.
  * 이 인증서에 대 한 특정 사항은 자체 서명 된 인증서 또는 CA 기관을 통해 프로 비전 인증서를 수 있습니다.
  * Powershell 또는 openssl과 같은 표준 도구를 통해 생성할 수 있습니다.
  * 대상 컴퓨터의 인증서 저장소에 설치 하거나 강력한 암호를 사용 하 여 pfx 파일로 배포 될 수 있습니다.

### <a name="example-deploy-into-azure-websites"></a>예제: Azure Websites에 배포

이 섹션의 인증서 저장소에 저장 된 인증서를 사용 하 여 Azure websites에 응용 프로그램을 배포 하려고 합니다. 인증서 저장소에서 인증서를 로드 하려면 응용 프로그램을 수정 해야 합니다. 이렇게 하려면이 app service 계획에서는 이후 단계에서 구성 하는 경우 표준 계층에서 최소 수 해야 합니다. 응용 프로그램에서 간단히 키 세부 정보를 포함 하는 appsettings.json IdentityServer 섹션을 수정 해야 합니다.
```json
  "IdentityServer": {
    "Key": {
      "Type": "Store",
      "StoreName": "My",
      "StoreLocation": "CurrentUser",
      "Name": "CN=MyApplication"
    }
  }
}
```
* 인증서 이름 속성의 고유 인증서의 주체를 사용 하 여 해당합니다.
* 저장소 위치 (CurrentUrser 또는 LocalMachine)에서 인증서를 로드할 수 있는 위치를 나타냅니다.
* 저장소 이름을는 개인 사용자 저장소를 가리키는 경우이 인증서가 저장 된 인증서 저장소의 이름을 나타냅니다.

Azure Websites에 배포 하려면의 단계에 따라 앱을 배포할 [Azure에 앱을 배포](xref:tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure) 필요한 Azure 리소스를 만들고 앱을 프로덕션에 배포 합니다.

이 작업을 수행한 후 응용 프로그램을 Azure에 배포 된 아닌 아직 완전히 작동 여전히 응용 프로그램에서 사용할 인증서를 설치 하는 데 필요 하기. 이렇게 하려면 우리가 해야 사용 하 고에 설명 된 단계를 수행 하려고 하는 인증서의 지문을 [인증서 로드](/azure/app-service/app-service-web-ssl-cert-load#load-your-certificates)합니다.

SSL 언급 하는이 단계를 하는 동안 "개인" 인증서"섹션에 있는지 포털 앱을 사용 하는 프로 비전된 인증서를 업로드할 수 있습니다.

이 단계를 수행한 후 응용 프로그램을 다시 시작할 수 있어야 하 고 완전히 작동 해야 합니다.

## <a name="other-configuration-options"></a>기타 구성 옵션
API 권한 부여에 대 한 지원과 규칙, 기본값 및 단일 페이지 응용 프로그램에 대 한 경험을 간소화 하기 위해 향상 된 기능 집합을 사용 하 여 Identity Server를 기반으로 작성 합니다. 물론 Identity Server의 모든 기능을 사용할 수 백그라운드는 제공 되는 통합 시나리오는 포함 되지 않습니다. 지원과 부르는 "타사" 응용 프로그램을 모든 응용 프로그램이 만들어지고 조직에서 배포 된 위치에 포커스가 있습니다. 따라서 동의 또는 페더레이션과 같은 항목에 대 한 지원을 제공 하지 않습니다. 이러한 시나리오 Identity Server를 사용 하 여 해당 설명서를 수행 하는 것이 좋습니다.

### <a name="application-profiles"></a>응용 프로그램 프로필
응용 프로그램 프로필은 추가 매개 변수를 정의 하는 응용 프로그램에 대 한 미리 정의 된 구성입니다. 지금은 두 프로필 지원합니다.
* IdentityServerSPA: Id 서버를 단일 단위로 함께 호스트 하는 단일 페이지 응용 프로그램을 나타냅니다.
  * 기본값은 redirect_uri `/authentication/login-callback`합니다.
  * 기본적으로 post_logout_redirect_uri `/authentication/logout-callback`합니다.
  * 범위 집합에 포함 됩니다는 `openid`, `profile`, 및 응용 프로그램에서 Api에 대해 정의 된 모든 범위입니다.
  * 허용 되는 OIDC 응답 형식 집합이 `id_token token` 또는 각각 개별적으로 (`id_token`, `token`).
  * 허용 되는 응답 모드는 `fragment`합니다.
* SPA: Identity Server를 사용 하 여 호스트 되지 않는 단일 페이지 응용 프로그램을 나타냅니다.
  * 범위 집합에 포함 됩니다는 `openid`, `profile`, 및 응용 프로그램에서 Api에 대해 정의 된 모든 범위입니다.
  * 허용 되는 OIDC 응답 형식 집합이 `id_token token` 또는 각각 개별적으로 (`id_token`, `token`).
  * 허용 되는 응답 모드는 `fragment`합니다.
* IdentityServerJwt: Identity Server를 사용 하 여 함께 호스트 되는 API를 나타냅니다.
  * 응용 프로그램을 기본 응용 프로그램 이름으로 단일 범위를 포함 하도록 구성 되어 있습니다.
* API: Identity Server를 사용 하 여 호스트 되지 않는 API를 나타냅니다.
  * 응용 프로그램을 기본 응용 프로그램 이름으로 단일 범위를 포함 하도록 구성 되어 있습니다.

### <a name="configuration-through-appsettings"></a>AppSettings 통해 구성
각각 클라이언트 또는 리소스 목록에 추가 하 여 구성 시스템을 통해 응용 프로그램을 구성할 수 있습니다. 

구성 하 여 클라이언트를 구성 하는 경우는 `redirect_uri` 하며 `post_logout_redirect_uri` 아래와 같이:
```json
  "IdentityServer": {
    "Clients": {
      "MySPA": {
        "Profile": "SPA",
        "RedirectUri": "https://www.example.com/authentication/login-callback",
        "LogoutUri": "https://www.example.com/authentication/logout-callback"
      }
    }
  }
```

리소스를 구성 하는 경우 아래와 같이 리소스의 범위를 구성할 수 있습니다.
```json
"IdentityServer": {
  "Resources": {
    "MyExternalApi": {
      "Profile": "API",
      "Scopes": "a b c",
    }
  }
}
```

### <a name="configuration-through-code"></a>코드를 통해 구성
클라이언트 및 AddApiAuthorization 옵션을 구성 하는 작업을 수행 하는 오버 로드를 사용 하 여 코드를 통해 리소스를 구성할 수도 있습니다.
```csharp
AddApiAuthorization<ApplicationUser, ApplicationDbContext>(options =>
{
    options.Clients.AddSPA(
        "My SPA",
        spa => spa.WithRedirectUri("http://www.example.com/authentication/login-callback")
            .WithLogoutRedirectUri("http://www.example.com/authentication/logout-callback"));

    options.ApiResources.AddApiResource("MyExternalApi", resource => resource.WithScopes("a", "b", "c"));
});
```
