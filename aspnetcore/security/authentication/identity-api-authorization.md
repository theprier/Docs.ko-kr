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
# <a name="authentication-and-authorization-for-spas"></a><span data-ttu-id="f06af-103">인증 및 Spa에 대 한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f06af-103">Authentication and authorization for SPAs</span></span>

<span data-ttu-id="f06af-104">ASP.NET 3.0에는 API 권한 부여에 대 한 새로운 지원을 통해,를 사용 하 여 단일 페이지 응용 프로그램의 인증에 대 한 지원이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-104">In ASP.NET 3.0 we are introducing support for authentication in single page applications using our new support for API authorization.</span></span> <span data-ttu-id="f06af-105">이 지원 됩니다 인증 하 고 Open ID Connect 구현에 대 한 사용자 및 Id 서버 저장 ASP.NET Core Id의 조합의 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-105">This support is based on a combination of ASP.NET Core Identity for authenticating and storing users and Identity Server for implementing Open ID Connect.</span></span>

<span data-ttu-id="f06af-106">새 인증 매개 변수는 Angular에 추가 했습니다 및 React 템플릿은 인증 매개 변수는 mvc 및 razor 페이지 템플릿 사용 하 여 유사한 허용 값 'None' 및 '개별'.</span><span class="sxs-lookup"><span data-stu-id="f06af-106">We have added a new authentication parameter to our Angular and React templates that is similar to the authentication parameter in our mvc and razor pages templates with allowed values 'None' and 'Individual'.</span></span>

## <a name="create-an-angular-app-with-api-authorization-support"></a><span data-ttu-id="f06af-107">API 권한 부여 지원을 통해 Angular 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f06af-107">Create an Angular app with API authorization support</span></span>

<span data-ttu-id="f06af-108">인증 및 사용자의 권한 부여를 지 원하는 새 Angular 앱을 만들려면 명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-108">To create a new Angular app with support for authentication and authorization of users, open a command shell and run the following command:</span></span>

```console
dotnet new angular -o <output_directory_name> -au Individual
```

<span data-ttu-id="f06af-109">앞의 명령을 사용 하 여 ASP.NET Core 앱을 만듭니다는 *ClientApp* Angular 앱이 포함 된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-109">The preceding command creates an ASP.NET Core app with a *ClientApp* directory containing the Angular app.</span></span>

## <a name="create-a-react-app-with-api-authorization-support"></a><span data-ttu-id="f06af-110">API 권한 부여 지원을 통해 React 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f06af-110">Create a React app with API authorization support</span></span>

<span data-ttu-id="f06af-111">인증 및 사용자의 권한 부여를 지 원하는 새 React 앱을 만들려면 명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-111">To create a new React app with support for authentication and authorization of users, open a command shell and run the following command:</span></span>

```console
dotnet new react -o <output_directory_name> -au Individual
```

<span data-ttu-id="f06af-112">앞의 명령을 사용 하 여 ASP.NET Core 앱을 만듭니다는 *ClientApp* React 앱이 포함 된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-112">The preceding command creates an ASP.NET Core app with a *ClientApp* directory containing the React app.</span></span>

## <a name="general-description-of-the-aspnet-core-components-of-the-app"></a><span data-ttu-id="f06af-113">앱의 ASP.NET Core 구성 요소에 대 한 일반적인 설명</span><span class="sxs-lookup"><span data-stu-id="f06af-113">General description of the ASP.NET Core components of the app</span></span>

<span data-ttu-id="f06af-114">인증에 대 한 지원을 포함 하는 경우 프로젝트에 대 한 몇 가지 추가 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-114">There are several additions to the project when we include support for authentication:</span></span>

### <a name="startup-class"></a><span data-ttu-id="f06af-115">Startup 클래스</span><span class="sxs-lookup"><span data-stu-id="f06af-115">Startup class</span></span>

<span data-ttu-id="f06af-116">아래 Startup 클래스의 코드를 살펴보면 다음 포함 드립니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-116">If we look at the code in the Startup class below we can appreciate the following inclusions:</span></span>
* <span data-ttu-id="f06af-117">내부 `public void ConfigureServices(IServiceCollection services)`:</span><span class="sxs-lookup"><span data-stu-id="f06af-117">Inside `public void ConfigureServices(IServiceCollection services)`:</span></span>
  * <span data-ttu-id="f06af-118">기본 UI 사용 하 여 id입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-118">Identity with the default UI.</span></span>
    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
      options.UseSqlite(Configuration.GetConnectionString("DefaultConnection")));

    services.AddDefaultIdentity<ApplicationUser>()
      .AddDefaultUI(UIFramework.Bootstrap4)
      .AddEntityFrameworkStores<ApplicationDbContext>();
    ```
  * <span data-ttu-id="f06af-119">Identity Server 추가 AddApiAuthorization 도우미 메서드를 사용 하 여 해당 설정 일부 기본 Identity Server를 기반으로 ASP.NET 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-119">Identity Server with an additional AddApiAuthorization helper method that setups some default ASP.NET Conventions on top of Identity Server.</span></span>
    ```csharp
    services.AddIdentityServer()
      .AddApiAuthorization<ApplicationUser, ApplicationDbContext>();
    ```
  * <span data-ttu-id="f06af-120">Identity Server에서 생성 된 Jwt 토큰의 유효성을 검사 하도록 응용 프로그램을 구성 하는 추가 AddIdentityServerJwt 도우미 메서드를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-120">Authentication with an additional AddIdentityServerJwt helper method that configures the application to validate Jwt tokens produced by Identity Server.</span></span> 
    ```csharp
    services.AddAuthentication()
      .AddIdentityServerJwt();
    ```
* <span data-ttu-id="f06af-121">내부 `public void Configure(IApplicationBuilder app)`:</span><span class="sxs-lookup"><span data-stu-id="f06af-121">Inside `public void Configure(IApplicationBuilder app)`:</span></span>
  * <span data-ttu-id="f06af-122">들어오는 요청에 자격 증명의 유효성을 검사 하 고 사용자 요청 컨텍스트를 설정 하는 일을 담당 하는 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-122">The authentication middleware that is responsible for validating the credentials in the incoming request and setting the user on the request context.</span></span>
    ```csharp
    app.UseAuthentication();
    ```
  * <span data-ttu-id="f06af-123">Open ID Connect 끝점을 노출 하는 identity server 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-123">The identity server middleware that exposes the Open ID Connect endpoints.</span></span>
    ```csharp
    app.UseIdentityServer();
    ```

### <a name="addapiauthorization"></a><span data-ttu-id="f06af-124">AddApiAuthorization</span><span class="sxs-lookup"><span data-stu-id="f06af-124">AddApiAuthorization</span></span> 
<span data-ttu-id="f06af-125">이 도우미 메서드는 지원 되는 구성을 사용 하려면 Id 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-125">This helper method configures Identity Server to use our supported configuration.</span></span> <span data-ttu-id="f06af-126">Identity Server 응용 프로그램 보안 문제를 처리 하기 위한 매우 강력 하 고 확장 가능한 프레임 워크 이지만 가장 일반적인 시나리오에 대해 알아야 할 필요 하지 않은 복잡성을 많이 노출 하는 동시에에 따라서 선택 규칙 집합 및 생각 하는 구성 옵션 좋은 시작 지점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-126">Identity Server is a very powerful and extensible framework for handling application security concerns but at the same time that exposes a lot of complexity that we don't need to know about for the most common scenarios, so we choose a set of conventions and configuration options for you that we consider are a good starting point.</span></span> <span data-ttu-id="f06af-127">인증 요구 사항이 변경 되 면 필요에 맞게 사용자 지정할 수 있습니다 Identity Server의 모든 기능을 여전히 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-127">Once your authentication needs change the full power of Identity Server is still available to you so you can customize it to suit your needs.</span></span>

### <a name="addidentityserverjwt"></a><span data-ttu-id="f06af-128">AddIdentityServerJwt</span><span class="sxs-lookup"><span data-stu-id="f06af-128">AddIdentityServerJwt</span></span>
<span data-ttu-id="f06af-129">이 도우미 메서드는 기본 인증 처리기로 응용 프로그램에 대 한 정책 구성표를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-129">This helper method configures a policy scheme for the application as the default authentication handler.</span></span> <span data-ttu-id="f06af-130">Identity Id url 공간에 모든 하위 경로로 이동 하는 모든 요청을 처리할 수 있도록 정책이 구성 되어 "/ Identity" 및 다른 모든 요청을 처리 JwtBearerHandler 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-130">The policy is configured to let identity handle all the requests that go to any subpath in the Identity url space "/Identity" and to let the JwtBearerHandler handle all other requests.</span></span>
<span data-ttu-id="f06af-131">Addionally이이 메서드는 등록을 `<<ApplicationName>>API` 의 기본 범위를 사용 하 여 id 서버를 사용 하 여 Api 리소스 `<<ApplicationName>>API` 하 고 응용 프로그램에 대 한 Identity Server에서 발급 된 토큰의 유효성을 검사 하 여 JWT 전달자 토큰 미들웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-131">Addionally this method registers an `<<ApplicationName>>API` Api resource with identity server with a default scope of `<<ApplicationName>>API` and configures the JWT Bearer token middleware to validate tokens issued by Identity Server for the application.</span></span>

### <a name="sampledatacontroller"></a><span data-ttu-id="f06af-132">SampleDataController</span><span class="sxs-lookup"><span data-stu-id="f06af-132">SampleDataController</span></span>
<span data-ttu-id="f06af-133">Controllers\SampleDataController.cs 파일에 살펴봅니다 것을 볼 수 있습니다는 `[Authorize]` 리소스에 액세스 하는 기본 정책을 기반으로 사용자 권한을 부여 해야 함을 나타내는 클래스에 적용 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-133">If we look at the file Controllers\SampleDataController.cs we can observe the `[Authorize]` attribute applied to the class that indicates that the user needs to be authorized based on the default policy to access the resource.</span></span> <span data-ttu-id="f06af-134">기본 권한 부여 정책을 통해 설정 되는 기본 인증 체계를 사용 하도록 구성 되어야 발생 `AddIdentityServerJwt` 위에서 설명한 정책 구성표를 하 여 JwtBearer 처리기 구성 이러한 도우미 메서드에서 대 한 기본 처리기 앱에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-134">The default authorization policy happens to be configured to use the default authentication scheme which is set up by `AddIdentityServerJwt` to the policy scheme that we mentioned above, making the JwtBearer handler configured by such helper method the default handler for requests to the app.</span></span>

### <a name="applicationdbcontext"></a><span data-ttu-id="f06af-135">ApplicationDbContext</span><span class="sxs-lookup"><span data-stu-id="f06af-135">ApplicationDbContext</span></span>
<span data-ttu-id="f06af-136">Data\ApplicationDbContext.cs에서 파일을 보면 알 수 있습니다 ApiAuthorizationDbContext (IdentityDbContext에서 더 많이 파생 된 클래스)를 확장 하는 예외를 사용 하 여 id에 사용 된 동일한 DbContext Identity Server에 대 한 스키마를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-136">If we look at the file in Data\ApplicationDbContext.cs we can see the same DbContext we use in identity with the exception that it extends ApiAuthorizationDbContext (a more derived class from IdentityDbContext) to include the schema for Identity Server.</span></span>
<span data-ttu-id="f06af-137">데이터베이스 스키마의 전체 제어 하려는 경우에서는 간단히 사용할 수 있는 Identity DbContext 클래스 중 하나에서 상속 하 고 구성할 수를 호출 하 여 id 스키마를 포함 하는 상황에 맞는 `builder.ConfigurePersistedGrantContext(_operationalStoreOptions.Value)` 에 `OnModelCreating` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f06af-137">If we want full control of the database schema we can simply inherit from one of the available Identity DbContext classes and configure the context to include the identity schema by calling `builder.ConfigurePersistedGrantContext(_operationalStoreOptions.Value)` on the `OnModelCreating` method.</span></span>

### <a name="oidcconfigurationcontroller"></a><span data-ttu-id="f06af-138">OidcConfigurationController</span><span class="sxs-lookup"><span data-stu-id="f06af-138">OidcConfigurationController</span></span>
<span data-ttu-id="f06af-139">보면 파일 끝점을 보면 Controllers\OidcConfigurationController.cs OIDC 매개 변수를 사용 해야 하는 클라이언트에 맞도록 기립 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-139">If we look at the file Controllers\OidcConfigurationController.cs we can see the endpoint that we stand-up to serve the OIDC parameters that the client needs to use.</span></span>

### <a name="appsettingsjson"></a><span data-ttu-id="f06af-140">appsettings.json</span><span class="sxs-lookup"><span data-stu-id="f06af-140">appsettings.json</span></span>
<span data-ttu-id="f06af-141">프로젝트의 루트에서 appsettings.json 파일을 보면 확인할 수 있습니다 새 `IdentityServer` 섹션 목록을 설명 하는 클라이언트를 구성 하 고 단일 클라이언트 인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-141">If we look at the appsettings.json file on the root of the project, we can see a new `IdentityServer` section that describes the list of configured clients and we can see that there is a single client.</span></span> <span data-ttu-id="f06af-142">클라이언트의 응용 프로그램의 이름에 해당 이름과 oAuth ClientId 매개 변수 규칙으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-142">The name of the client corresponds to the name of the application and is mapped by convention to the oAuth ClientId parameter.</span></span> <span data-ttu-id="f06af-143">프로필을 구성 하는 응용 프로그램의 유형을 나타냅니다 및 서버에 대 한 구성 프로세스를 간소화 하는 드라이브 규칙을 내부적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-143">The profile indicates what type of application we are configuring, and we use it internally to drive conventions that simplify the configuration process for the server.</span></span> <span data-ttu-id="f06af-144">몇 가지 사용 가능한 프로필 아래 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-144">There are several profiles available explained in the section below.</span></span>

```json
"IdentityServer": {
  "Clients": {
    "angularindividualpreview3final": {
      "Profile": "IdentityServerSPA"
    }
  }
}
```

### <a name="appsettingsdevelopmentjson"></a><span data-ttu-id="f06af-145">appsettings.Development.json</span><span class="sxs-lookup"><span data-stu-id="f06af-145">appsettings.Development.json</span></span>
<span data-ttu-id="f06af-146">Appsettings 보면. Development.json 파일 프로젝트의 루트를 보면 새 `IdentityServer` 토큰에 서명 하는 키를 설명 하는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-146">If we look at the appsettings.Development.json file on the root of the project, we can see a new `IdentityServer` section that describes the key we are using to sign tokens.</span></span> <span data-ttu-id="f06af-147">프로덕션에 배포 하는 경우 키를 프로 비전 하 고 아래 설명 된 대로 응용 프로그램과 함께 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-147">When deploying to production a key needs to be provisioned and deployed alongside the application as explained below.</span></span>

```json
  "IdentityServer": {
    "Key": {
      "Type": "Development"
    }
  }
}
```

## <a name="general-description-of-the-angular-application"></a><span data-ttu-id="f06af-148">Angular 응용 프로그램에 대 한 일반적인 설명</span><span class="sxs-lookup"><span data-stu-id="f06af-148">General description of the Angular application</span></span>
<span data-ttu-id="f06af-149">Angular 모듈 자체에 거주 하는 인증 및 Angular 템플릿은 API 권한 부여에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="f06af-149">The support for authentication and API authorization in the Angular template lives in its own Angular module.</span></span> <span data-ttu-id="f06af-150">ClientApp\src\api에 대 한 권한 부여 및 것 같습니다. 다음과 같은 요소로 구성</span><span class="sxs-lookup"><span data-stu-id="f06af-150">Under ClientApp\src\api-authorization and it is composed of the following elements:</span></span>
* <span data-ttu-id="f06af-151">구성 요소 3:</span><span class="sxs-lookup"><span data-stu-id="f06af-151">3 Components:</span></span>
  * <span data-ttu-id="f06af-152">로그인 구성 요소입니다. 앱에 대 한 로그인 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-152">Login component: Handles the login flow for the app.</span></span>
  * <span data-ttu-id="f06af-153">로그 아웃 구성 요소입니다. 앱에 대 한 로그 아웃 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-153">Logout component: Handles the logout flow for the app.</span></span>
  * <span data-ttu-id="f06af-154">로그인 메뉴 구성 요소: 현재 표시 된 위젯을 사용자 프로필을 관리 하 고 로그 아웃 링크를 사용 하 여 사용자를 인증 하거나 사용자가 인증 되지 않은 경우 등록 또는 로그인에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-154">Login menu component: A widget that displays the current authenticated user with links to manage the user profile and log out or links to log in or register when the user is not authenticated.</span></span>
* <span data-ttu-id="f06af-155">경로 가드 `AuthorizeGuard` 경로에 추가할 수 있습니다 하 고 사용자 경로 방문 하기 전에 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-155">A route guard `AuthorizeGuard` that can be added to routes and requires a user to be authenticated before visiting the route.</span></span>
* <span data-ttu-id="f06af-156">Http 인터셉터 `AuthorizeInterceptor` 사용자가 인증 하는 경우에 API를 대상으로 나가는 HTTP 요청에 액세스 토큰을 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-156">An http interceptor `AuthorizeInterceptor` that attaches the access token to outgoing HTTP requests targeting the API when the user is authenticated.</span></span>
* <span data-ttu-id="f06af-157">서비스 `AuthorizeService` 인증 프로세스의 더 낮은 수준의 세부 정보를 처리 하 고 소비 응용 프로그램의 나머지 부분에 인증된 된 사용자에 대 한 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-157">A service `AuthorizeService` that handles the lower level details of the authentication process and exposes information about the authenticated user to the rest of the application for consumption.</span></span>
* <span data-ttu-id="f06af-158">응용 프로그램의 인증 부분을 사용 하 여 연결 된 경로 정의 하 고 로그인 메뉴 구성 요소, 인터셉터, 가드 및 응용 프로그램의 나머지 부분에서 사용 하기 위해 서비스를 노출 하는 angular 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-158">An angular module that defines routes associated with the authentication parts of the application and exposes the login menu component, the interceptor, the guard and the service for consumption from the rest of the application.</span></span>

## <a name="general-description-of-the-react-application"></a><span data-ttu-id="f06af-159">React 응용 프로그램에 대 한 일반적인 설명</span><span class="sxs-lookup"><span data-stu-id="f06af-159">General description of the React application</span></span>
<span data-ttu-id="f06af-160">인증 및 React 템플릿은 생활 ClientApp\src\components\api authorization\ 하며 아래 API 권한 부여에 대 한 지원이 다음과 같은 요소로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-160">The support for authentication and API authorization in the React template lives under ClientApp\src\components\api-authorization\ and it is composed of the following elements:</span></span>
* <span data-ttu-id="f06af-161">4 개 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-161">4 Components:</span></span>
  * <span data-ttu-id="f06af-162">로그인 구성 요소입니다. 앱에 대 한 로그인 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-162">Login component: Handles the login flow for the app.</span></span>
  * <span data-ttu-id="f06af-163">로그 아웃 구성 요소입니다. 앱에 대 한 로그 아웃 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-163">Logout component: Handles the logout flow for the app.</span></span>
  * <span data-ttu-id="f06af-164">로그인 메뉴 구성 요소: 현재 표시 된 위젯을 사용자 프로필을 관리 하 고 로그 아웃 링크를 사용 하 여 사용자를 인증 하거나 사용자가 인증 되지 않은 경우 등록 또는 로그인에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-164">Login menu component: A widget that displays the current authenticated user with links to manage the user profile and log out or links to log in or register when the user is not authenticated.</span></span>
  * <span data-ttu-id="f06af-165">AuthorizeRoute: 사용자 구성 요소 매개 변수에 지정 된 구성 요소를 렌더링 하기 전에 인증을 요구 하는 경로 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-165">AuthorizeRoute: A route component that requires a user to be authenticated before rendering the component indicated in the Component parameter.</span></span>
  * <span data-ttu-id="f06af-166">내보낸 `authService` 클래스의 인스턴스 `AuthorizeService` 인증 프로세스의 더 낮은 수준의 세부 정보를 처리 하 고 소비 응용 프로그램의 나머지 부분에 인증된 된 사용자에 대 한 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-166">An exported `authService` instance of class `AuthorizeService` that handles the lower level details of the authentication process and exposes information about the authenticated user to the rest of the application for consumption.</span></span>

<span data-ttu-id="f06af-167">솔루션의 주요 구성 요소에서 살펴본 했으므로 응용 프로그램에 대 한 개별 시나리오에서 특정 모양으로 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-167">Now that we've seen the main components of the solution, we can take a specific look at individual scenarios for the application:</span></span>

## <a name="requiring-authorization-on-a-new-api"></a><span data-ttu-id="f06af-168">새 API에 필요한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f06af-168">Requiring authorization on a new API</span></span>
<span data-ttu-id="f06af-169">시스템은 새 Api에 대 한 권한 부여를 요구 하도록 trivial 되도록 기본적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-169">The system is configured out of the box to make it trivial to require authorization for new APIs.</span></span> <span data-ttu-id="f06af-170">이렇게 하려면 단순히 새 컨트롤러를 만들고 추가 `[Authorize]` 특성을 컨트롤러 클래스 또는 컨트롤러 내의 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-170">In order to do so, simply create a new controller and add the `[Authorize]` attribute to the controller class or to any action within the controller.</span></span>

## <a name="protecting-a-client-side-route-angular"></a><span data-ttu-id="f06af-171">클라이언트 쪽 경로 (Angular) 보호</span><span class="sxs-lookup"><span data-stu-id="f06af-171">Protecting a client-side route (Angular)</span></span>
<span data-ttu-id="f06af-172">클라이언트 쪽 경로 보호는 권한 부여 보호에 경로 구성 하는 경우를 실행 하는 가드의 목록에 추가 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-172">Protecting a client side route is done by adding the authorize guard to the list of guards to run when configuring a route.</span></span> <span data-ttu-id="f06af-173">예를 들어 기본 앱 angular 모듈 내에서 데이터를 가져오고 경로 구성 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-173">As an example you can see how the fetch-data route is configured within the main app angular module:</span></span>

```ts
RouterModule.forRoot([
  // ...
  { path: 'fetch-data', component: FetchDataComponent, canActivate: [AuthorizeGuard] },
])
```

<span data-ttu-id="f06af-174">경로 보호 합니다. 실제 끝점을 보호 하지 않습니다 언급 해야 (여전히 필요는 `[Authorize]` 특성이 적용) 있지만 해당만 사용자가 인증 되지 않은 경우 지정 된 클라이언트 쪽 경로 탐색에서 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-174">It is important to mention that protecting a route doesn't protect the actual endpoint (which still requires an `[Authorize]` attribute applied to it) but that it only prevents the user from navigating to the given client side route when it is not authenticated.</span></span>

## <a name="authenticate-api-requests-angular"></a><span data-ttu-id="f06af-175">API 요청 (Angular) 인증</span><span class="sxs-lookup"><span data-stu-id="f06af-175">Authenticate API requests (Angular)</span></span>

<span data-ttu-id="f06af-176">응용 프로그램은 HTTP 클라이언트 응용 프로그램에서 정의 된 인터셉터를 사용 하 여 자동으로 수행 됩니다 함께 호스트 되는 Api에 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-176">Authenticating requests to APIs hosted along side the application is done automatically through the use of the HTTP client interceptor defined by the application.</span></span>

## <a name="protect-a-client-side-route-react"></a><span data-ttu-id="f06af-177">클라이언트 쪽 경로 (React) 보호</span><span class="sxs-lookup"><span data-stu-id="f06af-177">Protect a client-side route (React)</span></span>

<span data-ttu-id="f06af-178">클라이언트 쪽 경로 보호 하는 일반 경로 구성 요소 대신 AuthorizeRoute 구성 요소를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-178">Protecting a client side route is done by using the AuthorizeRoute component instead of the plain Route component.</span></span> <span data-ttu-id="f06af-179">예를 들어 앱 구성 요소 내에서 데이터를 가져오고 경로 구성 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-179">As an example you can see how the fetch-data route is configured within the App component:</span></span>

```jsx
<AuthorizeRoute path='/fetch-data' component={FetchData} />
```

<span data-ttu-id="f06af-180">경로 보호 합니다. 실제 끝점을 보호 하지 않습니다 언급 해야 (여전히 필요는 `[Authorize]` 특성이 적용) 있지만 해당만 사용자가 인증 되지 않은 경우 지정 된 클라이언트 쪽 경로 탐색에서 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-180">It is important to mention that protecting a route doesn't protect the actual endpoint (which still requires an `[Authorize]` attribute applied to it) but that it only prevents the user from navigating to the given client side route when it is not authenticated.</span></span>

## <a name="authenticate-api-requests-react"></a><span data-ttu-id="f06af-181">API 요청 (React) 인증</span><span class="sxs-lookup"><span data-stu-id="f06af-181">Authenticate API requests (React)</span></span>

<span data-ttu-id="f06af-182">먼저 이루어집니다 react 사용 하 여 요청을 인증 합니다 `authService` 에서 인스턴스는 `AuthorizeService` 는 authService에서 액세스 토큰을 검색 하 고 아래와 같이 요청에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-182">Authenticating requests with react is done by first importing the `authService` instance from the `AuthorizeService` and then retrieving the access token from the authService and attaching it to the request as shown below.</span></span> <span data-ttu-id="f06af-183">React 구성 요소에서 일반적으로 이렇게 componentDidMount 수명 주기 메서드 또는 결과에서 일부 사용자 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-183">In react components this is typically done in the componentDidMount lifecycle method or as the result from some user interaction.</span></span>

### <a name="import-the-authservice-into-your-component"></a><span data-ttu-id="f06af-184">구성 요소에는 authService 가져오기</span><span class="sxs-lookup"><span data-stu-id="f06af-184">Import the authService into your component</span></span>

```js
import authService from './api-authorization/AuthorizeService'
```

### <a name="retrieve-and-attach-the-access-token-to-the-response"></a><span data-ttu-id="f06af-185">검색 및 액세스 토큰 응답에 연결</span><span class="sxs-lookup"><span data-stu-id="f06af-185">Retrieve and attach the access token to the response</span></span>

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

## <a name="deploy-into-production"></a><span data-ttu-id="f06af-186">프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="f06af-186">Deploy into production</span></span>

<span data-ttu-id="f06af-187">프로덕션 환경에 응용 프로그램을 배포 하기 위해 몇 가지 리소스를 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-187">In order to deploy the application into production we need to provision several resources:</span></span>
* <span data-ttu-id="f06af-188">Identity 사용자 계정 및 id 서버를 저장할 데이터베이스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-188">A database to store the Identity user accounts and the identity server grants.</span></span>
* <span data-ttu-id="f06af-189">프로덕션 인증서를 토큰 서명에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-189">A production certificate to use for signing tokens.</span></span>
  * <span data-ttu-id="f06af-190">이 인증서에 대 한 특정 사항은 자체 서명 된 인증서 또는 CA 기관을 통해 프로 비전 인증서를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-190">There are no specific requirements for this certificate; it can be a self-signed certificate or a certificate provisioned through a CA authority.</span></span>
  * <span data-ttu-id="f06af-191">Powershell 또는 openssl과 같은 표준 도구를 통해 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-191">It can be generated through standard tools like powershell or openssl.</span></span>
  * <span data-ttu-id="f06af-192">대상 컴퓨터의 인증서 저장소에 설치 하거나 강력한 암호를 사용 하 여 pfx 파일로 배포 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-192">It can be installed into the certificate store on the target machines or deployed as a pfx file with a strong password.</span></span>

### <a name="example-deploy-into-azure-websites"></a><span data-ttu-id="f06af-193">예제: Azure Websites에 배포</span><span class="sxs-lookup"><span data-stu-id="f06af-193">Example: Deploy into Azure Websites</span></span>

<span data-ttu-id="f06af-194">이 섹션의 인증서 저장소에 저장 된 인증서를 사용 하 여 Azure websites에 응용 프로그램을 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-194">In this section we are going to deploy the application to Azure websites using a certificate stored in the certificate store.</span></span> <span data-ttu-id="f06af-195">인증서 저장소에서 인증서를 로드 하려면 응용 프로그램을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-195">We need to modify the application to load a certicate from the certificate store.</span></span> <span data-ttu-id="f06af-196">이렇게 하려면이 app service 계획에서는 이후 단계에서 구성 하는 경우 표준 계층에서 최소 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-196">To do so, our app service plan needs to be at least on the standard tier when we configure in a later step.</span></span> <span data-ttu-id="f06af-197">응용 프로그램에서 간단히 키 세부 정보를 포함 하는 appsettings.json IdentityServer 섹션을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-197">In our application we simply need to modify the IdentityServer section on appsettings.json to include the key details:</span></span>
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
* <span data-ttu-id="f06af-198">인증서 이름 속성의 고유 인증서의 주체를 사용 하 여 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-198">The name property on certificate corresponds with the distinguished subject for the certificate.</span></span>
* <span data-ttu-id="f06af-199">저장소 위치 (CurrentUrser 또는 LocalMachine)에서 인증서를 로드할 수 있는 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-199">The store location represents where to load the certificate from (CurrentUrser or LocalMachine).</span></span>
* <span data-ttu-id="f06af-200">저장소 이름을는 개인 사용자 저장소를 가리키는 경우이 인증서가 저장 된 인증서 저장소의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-200">The store name represents the name of the certificate store where the certificate is stored, in this case it points to the personal user store.</span></span>

<span data-ttu-id="f06af-201">Azure Websites에 배포 하려면의 단계에 따라 앱을 배포할 [Azure에 앱을 배포](xref:tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure) 필요한 Azure 리소스를 만들고 앱을 프로덕션에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-201">To deploy to Azure Websites, deploy the app following the steps in [Deploy the app to Azure](xref:tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure) to create the necessary Azure resources and deploy the app to production.</span></span>

<span data-ttu-id="f06af-202">이 작업을 수행한 후 응용 프로그램을 Azure에 배포 된 아닌 아직 완전히 작동 여전히 응용 프로그램에서 사용할 인증서를 설치 하는 데 필요 하기.</span><span class="sxs-lookup"><span data-stu-id="f06af-202">After doing this, the application is deployed into Azure but is not yet completely functional as we still need to setup the certificate to be used by the application.</span></span> <span data-ttu-id="f06af-203">이렇게 하려면 우리가 해야 사용 하 고에 설명 된 단계를 수행 하려고 하는 인증서의 지문을 [인증서 로드](/azure/app-service/app-service-web-ssl-cert-load#load-your-certificates)합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-203">To do so, we need to have the thumbprint for the certificate we are going to use and follow the steps described in [Load your certificates](/azure/app-service/app-service-web-ssl-cert-load#load-your-certificates).</span></span>

<span data-ttu-id="f06af-204">SSL 언급 하는이 단계를 하는 동안 "개인" 인증서"섹션에 있는지 포털 앱을 사용 하는 프로 비전된 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-204">While these steps mention SSL, there is a "Private certificates" section on the portal where we can upload our provisioned certificate to use with our app.</span></span>

<span data-ttu-id="f06af-205">이 단계를 수행한 후 응용 프로그램을 다시 시작할 수 있어야 하 고 완전히 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-205">After this step, we should be able to restart our application and it should be completely functional.</span></span>

## <a name="other-configuration-options"></a><span data-ttu-id="f06af-206">기타 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="f06af-206">Other configuration options</span></span>
<span data-ttu-id="f06af-207">API 권한 부여에 대 한 지원과 규칙, 기본값 및 단일 페이지 응용 프로그램에 대 한 경험을 간소화 하기 위해 향상 된 기능 집합을 사용 하 여 Identity Server를 기반으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-207">Our support for API authorization builds on top of Identity Server with a set of conventions, default values and enhancements to simplify the experience for Single Page Applications.</span></span> <span data-ttu-id="f06af-208">물론 Identity Server의 모든 기능을 사용할 수 백그라운드는 제공 되는 통합 시나리오는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-208">Needless to say, the full power of Identity Server is available behind the scenes if the integrations that we offer don't cover your scenario.</span></span> <span data-ttu-id="f06af-209">지원과 부르는 "타사" 응용 프로그램을 모든 응용 프로그램이 만들어지고 조직에서 배포 된 위치에 포커스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-209">Our support is focused on what we call "first-party" applications, where all the applications are created and deployed by our organization.</span></span> <span data-ttu-id="f06af-210">따라서 동의 또는 페더레이션과 같은 항목에 대 한 지원을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-210">As such we don't offer support for things like consent or federation.</span></span> <span data-ttu-id="f06af-211">이러한 시나리오 Identity Server를 사용 하 여 해당 설명서를 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-211">For those scenarios our recommendation is to use Identity Server and follow their documentation.</span></span>

### <a name="application-profiles"></a><span data-ttu-id="f06af-212">응용 프로그램 프로필</span><span class="sxs-lookup"><span data-stu-id="f06af-212">Application profiles</span></span>
<span data-ttu-id="f06af-213">응용 프로그램 프로필은 추가 매개 변수를 정의 하는 응용 프로그램에 대 한 미리 정의 된 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-213">Application profiles are predefined configurations for applications that further define their parameters.</span></span> <span data-ttu-id="f06af-214">지금은 두 프로필 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-214">At this time we support two profiles:</span></span>
* <span data-ttu-id="f06af-215">IdentityServerSPA: Id 서버를 단일 단위로 함께 호스트 하는 단일 페이지 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-215">IdentityServerSPA: Represents a single page application hosted alongside Identity Server as a single unit.</span></span>
  * <span data-ttu-id="f06af-216">기본값은 redirect_uri `/authentication/login-callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-216">The redirect_uri defaults to `/authentication/login-callback`.</span></span>
  * <span data-ttu-id="f06af-217">기본적으로 post_logout_redirect_uri `/authentication/logout-callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-217">The post_logout_redirect_uri defaults to `/authentication/logout-callback`.</span></span>
  * <span data-ttu-id="f06af-218">범위 집합에 포함 됩니다는 `openid`, `profile`, 및 응용 프로그램에서 Api에 대해 정의 된 모든 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-218">The set of scopes includes the `openid`, `profile`, and every scope defined for the APIs in the application.</span></span>
  * <span data-ttu-id="f06af-219">허용 되는 OIDC 응답 형식 집합이 `id_token token` 또는 각각 개별적으로 (`id_token`, `token`).</span><span class="sxs-lookup"><span data-stu-id="f06af-219">The set of allowed OIDC response types is `id_token token` or each of them individually (`id_token`, `token`).</span></span>
  * <span data-ttu-id="f06af-220">허용 되는 응답 모드는 `fragment`합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-220">The allowed response mode is `fragment`.</span></span>
* <span data-ttu-id="f06af-221">SPA: Identity Server를 사용 하 여 호스트 되지 않는 단일 페이지 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-221">SPA: Represents a single page application that is not hosted with Identity Server.</span></span>
  * <span data-ttu-id="f06af-222">범위 집합에 포함 됩니다는 `openid`, `profile`, 및 응용 프로그램에서 Api에 대해 정의 된 모든 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-222">The set of scopes includes the `openid`, `profile`, and every scope defined for the APIs in the application.</span></span>
  * <span data-ttu-id="f06af-223">허용 되는 OIDC 응답 형식 집합이 `id_token token` 또는 각각 개별적으로 (`id_token`, `token`).</span><span class="sxs-lookup"><span data-stu-id="f06af-223">The set of allowed OIDC response types is `id_token token` or each of them individually (`id_token`, `token`).</span></span>
  * <span data-ttu-id="f06af-224">허용 되는 응답 모드는 `fragment`합니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-224">The allowed response mode is `fragment`.</span></span>
* <span data-ttu-id="f06af-225">IdentityServerJwt: Identity Server를 사용 하 여 함께 호스트 되는 API를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-225">IdentityServerJwt: Represents an API that is hosted alongside with Identity Server.</span></span>
  * <span data-ttu-id="f06af-226">응용 프로그램을 기본 응용 프로그램 이름으로 단일 범위를 포함 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-226">The application is configured to have a single scope that defaults to the application name.</span></span>
* <span data-ttu-id="f06af-227">API: Identity Server를 사용 하 여 호스트 되지 않는 API를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-227">API: Represents an API that is not hosted with Identity Server.</span></span>
  * <span data-ttu-id="f06af-228">응용 프로그램을 기본 응용 프로그램 이름으로 단일 범위를 포함 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-228">The application is configured to have a single scope that defaults to the application name.</span></span>

### <a name="configuration-through-appsettings"></a><span data-ttu-id="f06af-229">AppSettings 통해 구성</span><span class="sxs-lookup"><span data-stu-id="f06af-229">Configuration through AppSettings</span></span>
<span data-ttu-id="f06af-230">각각 클라이언트 또는 리소스 목록에 추가 하 여 구성 시스템을 통해 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-230">We can configure the applications through our configuration system by adding them to the list of Clients or Resources respectively.</span></span> 

<span data-ttu-id="f06af-231">구성 하 여 클라이언트를 구성 하는 경우는 `redirect_uri` 하며 `post_logout_redirect_uri` 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="f06af-231">When configuring clients we can configure the `redirect_uri` and the `post_logout_redirect_uri` as shown below:</span></span>
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

<span data-ttu-id="f06af-232">리소스를 구성 하는 경우 아래와 같이 리소스의 범위를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-232">When configuring resources we can configure the scopes for the resource as shown below:</span></span>
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

### <a name="configuration-through-code"></a><span data-ttu-id="f06af-233">코드를 통해 구성</span><span class="sxs-lookup"><span data-stu-id="f06af-233">Configuration through code</span></span>
<span data-ttu-id="f06af-234">클라이언트 및 AddApiAuthorization 옵션을 구성 하는 작업을 수행 하는 오버 로드를 사용 하 여 코드를 통해 리소스를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f06af-234">We can also configure the clients and resources through code using an overload of AddApiAuthorization that takes an action to configure options.</span></span>
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
