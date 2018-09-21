---
title: JavaScriptServices를 사용 하 여 ASP.NET Core의 단일 페이지 응용 프로그램을 만들려면
author: scottaddie
description: JavaScriptServices를 사용 하 여 단일 페이지 응용 프로그램 (SPA) ASP.NET Core에서 지 원하는 만들려면의 이점에 대해 알아봅니다.
ms.author: scaddie
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
uid: client-side/spa-services
ms.openlocfilehash: 6d6a92427d5d4b853248e60a12625573c4375515
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523300"
---
# <a name="use-javascriptservices-to-create-single-page-applications-in-aspnet-core"></a>JavaScriptServices를 사용 하 여 ASP.NET Core의 단일 페이지 응용 프로그램을 만들려면

하 여 [Scott Addie](https://github.com/scottaddie) 고 [Fiyaz Hasan](http://fiyazhasan.me/)

단일 페이지 응용 프로그램 (SPA)에 내재 된 풍부한 사용자 경험으로 인해 웹 응용 프로그램의 인기 있는 형식입니다. 클라이언트 쪽 SPA 프레임 워크 또는 라이브러리와 같은 통합 [Angular](https://angular.io/) 또는 [반응](https://facebook.github.io/react/), ASP.NET Core 어려울 수와 같은 서버 쪽 프레임 워크를 사용 하 여 합니다. [JavaScriptServices](https://github.com/aspnet/JavaScriptServices) 통합 프로세스의 마찰을 줄이기 위해 개발 되었습니다. 클라이언트 및 서버 기술 스택 간의 원활한 작업 수 있습니다.

<a name="what-is-js-services"></a>

## <a name="what-is-javascriptservices"></a>JavaScriptServices 란

JavaScriptServices는 ASP.NET Core에 대 한 클라이언트 쪽 기술 컬렉션입니다. ASP.NET Core Spa를 구축 하기 위한 개발자의 기본 서버 쪽 플랫폼으로 배치 하려면 해당 목표가입니다.

JavaScriptServices 세 가지 고유 NuGet 패키지 이루어져 있습니다.

* [Microsoft.AspNetCore.NodeServices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)
* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)
* [Microsoft.AspNetCore.SpaTemplates](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)

이러한 패키지는 유용한 경우 있습니다.

* 서버에서 JavaScript를 실행 합니다.
* SPA 프레임 워크 나 라이브러리를 사용 하 여
* Webpack 사용 하 여 클라이언트 쪽 자산 빌드

이 문서에 포커스를 많은 SpaServices 패키지를 사용 하 여 배치 됩니다.

<a name="what-is-spa-services"></a>

## <a name="what-is-spaservices"></a>SpaServices 란

ASP.NET Core Spa를 구축 하기 위한 개발자의 기본 서버 쪽 플랫폼으로 배치 하려면 SpaServices 만들어졌습니다. SpaServices 개발 ASP.NET Core를 사용 하 여 Spa를 필요 하지 않습니다 하 고 특정 클라이언트 프레임 워크에 사용자를 잠글 하지 않습니다.

SpaServices 같은 유용한 인프라를 제공 합니다.

* [서버 쪽 사전 렌더링이](#server-prerendering)
* [Webpack 개발 미들웨어](#webpack-dev-middleware)
* [핫 모듈 교체](#hot-module-replacement)
* [라우팅 도우미](#routing-helpers)

종합적으로 이러한 인프라 구성 요소 개발 워크플로 및 런타임 환경을 모두 향상 합니다. 구성 요소를 개별적으로 사용할 수 있습니다.

<a name="spa-services-prereqs"></a>

## <a name="prerequisites-for-using-spaservices"></a>SpaServices 사용 하기 위한 필수 구성 요소

SpaServices를 사용 하려면 다음을 설치 합니다.

* [Node.js](https://nodejs.org/) (버전 6 이상) npm을 사용 하 여
  * 이러한 구성 요소 설치 되 고 있을 수를 확인 하려면 명령줄에서 다음을 실행 합니다.

    ```console
    node -v && npm -v
    ```

참고: Azure 웹 사이트에 배포 하는 경우 필요가 여기에서 모든 작업을 수행할 &mdash; Node.js 설치 되어 서버 환경에서 사용할 수 있습니다.

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]

  * Visual Studio 2017을 사용 하 여 Windows를 사용 하는 경우 SDK가 선택 하 여 설치 합니다 **.NET Core 플랫폼 간 개발** 워크 로드.

* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet 패키지

<a name="server-prerendering"></a>

## <a name="server-side-prerendering"></a>서버 쪽 사전 렌더링이

유니버설 (라고도 해) 응용 프로그램을는 JavaScript 응용 프로그램 서버와 클라이언트 둘 다 실행 될 수 있습니다. Angular, React 및 기타 인기 있는 프레임 워크에는이 응용 프로그램 개발 스타일에 대 한 유니버설 플랫폼을 제공합니다. 먼저 Node.js 통해 서버에서 프레임 워크 구성 요소를 렌더링 하 고 클라이언트를 실행 한 다음 대리자 추가 하는 개념이입니다.

ASP.NET Core [태그 도우미](xref:mvc/views/tag-helpers/intro) 제공한 SpaServices 서버에서 JavaScript 함수를 호출 하 여 서버 쪽 사전 렌더링이 구현을 간소화 합니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [aspnet 사전 렌더링이](https://www.npmjs.com/package/aspnet-prerendering) npm 패키지:

    ```console
    npm i -S aspnet-prerendering
    ```

### <a name="configuration"></a>구성

프로젝트의 태그 도우미는 네임 스페이스 등록을 통해 검색할 내용이 *_ViewImports.cshtml* 파일:

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]

이러한 태그 도우미는 HTML 형식의 구문을 Razor 뷰 내에서 활용 하 여 하위 수준 Api와 직접 통신의 복잡성을 추상화 합니다.

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]

### <a name="the-asp-prerender-module-tag-helper"></a>`asp-prerender-module` 태그 도우미

합니다 `asp-prerender-module` 앞의 코드 예제에 사용 되는 태그 도우미를 실행 *ClientApp/dist/main-server.js* Node.js 통해 서버에 있습니다. 말씀 드리지만 대 한 *기본 server.js* 파일이 TypeScript-JavaScript 소스 간 컴파일 태스크의 아티팩트를 [Webpack](http://webpack.github.io/) 빌드 프로세스입니다. 항목 지점 별칭을 정의 하는 Webpack `main-server`;이 별칭에 대 한 종속성 그래프 순회를 시작 및 합니다 *ClientApp/부팅-server.ts* 파일:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]

예에서 다음 Angular를 *ClientApp/부팅-server.ts* 파일 활용 합니다 `createServerRenderer` 함수 및 `RenderResult` 유형의 `aspnet-prerendering` Node.js 통해 서버 렌더링을 구성 하려면 npm 패키지. 보내는 서버 쪽 렌더링은 강력한 JavaScript에 래핑되는 해결 함수 호출에 전달 되는 HTML 태그 `Promise` 개체입니다. `Promise` 개체의 중요 한 이유는 DOM의 자리 표시자 요소에 주입을 위한 페이지에 HTML 태그를 비동기적으로 제공 합니다.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]

### <a name="the-asp-prerender-data-tag-helper"></a>`asp-prerender-data` 태그 도우미

와 결합 하면 합니다 `asp-prerender-module` 태그 도우미는 `asp-prerender-data` 태그 도우미는 Razor 보기에서 컨텍스트 정보를 서버 쪽 JavaScript 전달할 데 사용할 수 있습니다. 다음 태그는 사용자 데이터를 전달 하는 예를 들어를 `main-server` 모듈:

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]

받은 `UserName` 인수는 기본 제공 JSON 직렬 변환기를 사용 하 여 직렬화 되 고에 저장 됩니다는 `params.data` 개체입니다. 다음 예제의 Angular, 데이터 내에서 개인 설정 된 인사말을 생성 하는 데 사용 된 `h1` 요소:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]

참고: 태그 도우미에 전달 된 속성 이름으로 표시 됩니다 **PascalCase** 표기법입니다. JavaScript에서 동일한 속성 이름으로 표시 됩니다는 위치와 달리 **camelCase**합니다. 기본 JSON serialization 구성이이 차이 담당합니다.

시 앞의 코드 예제를 확장 하려면 데이터로 전달할 수는 서버에서 보기로 hydrating 합니다 `globals` 속성에 제공 되는 `resolve` 함수:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]

`postList` 배열 내에 정의 된 `globals` 개체는 전역 브라우저의 연결 된 `window` 개체. 전역 범위에이 변수 호이스팅 제거 일일이, 특히 서버에서 한 번 및 클라이언트에서 다시 동일한 데이터를 로드 하는 관련 된 것입니다.

![창 개체에 연결 된 전역 postList 변수](spa-services/_static/global_variable.png)

<a name="webpack-dev-middleware"></a>

## <a name="webpack-dev-middleware"></a>Webpack 개발 미들웨어

[Webpack 개발 미들웨어](https://webpack.github.io/docs/webpack-dev-middleware.html) Webpack 주문형 리소스를 작성 하는 반면 간소화 된 개발 워크플로 소개 합니다. 미들웨어가 자동으로 컴파일하고 브라우저에서 페이지를 다시 로드 되 면 클라이언트 쪽 리소스를 제공 합니다. 대체 방법은 타사 종속성 또는 사용자 지정 코드를 변경 하는 경우 프로젝트의 npm 빌드 스크립트를 통해 Webpack를 수동으로 호출할 것입니다. Npm에서 스크립트를 작성 합니다 *package.json* 파일 다음 예제에 표시 됩니다.

```json
"build": "npm run build:vendor && npm run build:custom",
```

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [aspnet webpack](https://www.npmjs.com/package/aspnet-webpack) npm 패키지:

    ```console
    npm i -D aspnet-webpack
    ```

### <a name="configuration"></a>구성

Webpack 개발 미들웨어에서 다음 코드를 통해 HTTP 요청 파이프라인에 등록 합니다 *Startup.cs* 파일의 `Configure` 메서드:

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=webpack-middleware-registration&highlight=4)]

합니다 `UseWebpackDevMiddleware` 확장 메서드를 호출 하기 전에 [정적 파일 호스팅 등록](xref:fundamentals/static-files) 를 통해는 `UseStaticFiles` 확장 메서드. 보안상의 이유로 앱이 개발 모드에서 실행 하는 경우에 미들웨어를 등록 합니다.

합니다 *webpack.config.js* 파일의 `output.publicPath` 속성에 시청 하도록 미들웨어에 지시 합니다 `dist` 변경에 대 한 폴더:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]

<a name="hot-module-replacement"></a>

## <a name="hot-module-replacement"></a>핫 모듈 교체

Webpack의 생각할 [핫 모듈 교체](https://webpack.js.org/concepts/hot-module-replacement/) 진화 한 것으로 (HMR) 기능 [Webpack 개발 미들웨어](#webpack-dev-middleware)합니다. HMR 혜택을 모두 동일한을 소개 하지만 추가 변경 내용을 컴파일한 후 페이지 콘텐츠를 자동으로 업데이트 하 여 개발 워크플로 간소화 합니다. 현재 메모리 상태 및 SPA의 디버깅 세션을 사용 하 여 방해 하 게 브라우저의 새로 고침을 사용 하 여이 혼동 하지 마세요. Webpack 개발 미들웨어 서비스 및 브라우저에 변경 내용이 푸시 즉 브라우저 간에 실시간 연결 방법이 있습니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [webpack 실행 부하 과다 미들웨어](https://www.npmjs.com/package/webpack-hot-middleware) npm 패키지:

    ```console
    npm i -D webpack-hot-middleware
    ```

### <a name="configuration"></a>구성

HMR 구성 요소에서 MVC의 HTTP 요청 파이프라인에 등록 해야 합니다는 `Configure` 메서드:

```csharp
app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
    HotModuleReplacement = true
});
```

가 사용 하 여 true로 [Webpack 개발 미들웨어](#webpack-dev-middleware)의 `UseWebpackDevMiddleware` 확장 메서드를 호출 하기 전에 `UseStaticFiles` 확장 메서드. 보안상의 이유로 앱이 개발 모드에서 실행 하는 경우에 미들웨어를 등록 합니다.

합니다 *webpack.config.js* 파일을 정의 해야 합니다는 `plugins` 비워 두면 하는 경우에 배열:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]

브라우저에서 앱을 로드 한 후 개발자 도구 콘솔 탭 HMR 활성화에 대 한 확인을 제공 합니다.

![핫 모듈 교체 연결 된 메시지](spa-services/_static/hmr_connected.png)

<a name="routing-helpers"></a>

## <a name="routing-helpers"></a>라우팅 도우미

대부분의 ASP.NET Core 기반 Spa 서버 쪽 라우팅 외에도 클라이언트 쪽 라우팅을 해야 합니다. SPA 및 MVC 라우팅 시스템 간섭 하지 않고 독립적으로 작업할 수 있습니다. 그러나 방법이, 문제 하나에 지 사례 해답: 404 HTTP 응답을 식별 합니다.

있는 경우를 생각해 볼의 확장명 없는 경로 `/some/page` 사용 됩니다. 요청 하지 패턴 일치는 서버 쪽 경로 하지만 해당 패턴에는 클라이언트 쪽 경로 맞지 가정 합니다. 에 대 한 들어오는 요청을 살펴보겠습니다 `/images/user-512.png`, 일반적으로 서버의 이미지 파일을 찾으려고 시도입니다. 클라이언트 쪽 응용 프로그램에서 처리는 그럴 가능성은 요청 된 리소스 경로는 모든 서버 쪽 경로 또는 정적 파일와 일치 하지 않으면,-일반적으로 404 HTTP 상태 코드를 반환 하려고 합니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* 클라이언트 쪽 라우팅 npm 패키지입니다. 예를 들어 Angular를 사용합니다.

    ```console
    npm i -S @angular/router
    ```

### <a name="configuration"></a>구성

라는 확장 메서드 `MapSpaFallbackRoute` 에 사용 되는 `Configure` 메서드:

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=mvc-routing-table&highlight=7-9)]

팁: 경로 구성 하는 순서 대로 평가 됩니다. 결과적으로 `default` 패턴 일치를 위해 이전 코드 예제의 경로 먼저 사용 합니다.

<a name="new-project-creation"></a>

## <a name="creating-a-new-project"></a>새 프로젝트 만들기

JavaScriptServices에 미리 구성 된 응용 프로그램 템플릿을 제공합니다. SpaServices 다양 한 프레임 워크 및 Angular, React 및 Redux 등의 라이브러리와 함께에서 이러한 템플릿에서 사용 됩니다.

이러한 템플릿은 다음 명령을 실행 하 여.NET Core CLI를 통해 설치할 수 있습니다.

```console
dotnet new --install Microsoft.AspNetCore.SpaTemplates::*
```

사용 가능한 SPA 템플릿 목록이 표시 됩니다.

| 템플릿                                 | 짧은 이름 | 언어 | Tags        |
|:------------------------------------------|:-----------|:---------|:------------|
| Angular를 사용 하 여 ASP.NET Core MVC             | angular    | [C#]     | 웹/MVC/SPA |
| MVC ASP.NET Core (react.js 사용)            | react      | [C#]     | 웹/MVC/SPA |
| React.js 및 Redux MVC ASP.NET Core  | reactredux | [C#]     | 웹/MVC/SPA |

SPA 템플릿 중 하나를 사용 하 여 새 프로젝트를 만들려면 다음을 포함 합니다 **약식 이름** 에서 템플릿의 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령입니다. 다음 명령은 서버 쪽에 대해 구성 된 ASP.NET Core MVC를 사용 하 여 Angular 응용 프로그램을 만듭니다.

```console
dotnet new angular
```

<a name="runtime-config-mode"></a>

### <a name="set-the-runtime-configuration-mode"></a>런타임 구성 모드 설정

다음과 같은 두 가지 기본 런타임 구성 모드

* **개발**:
  * 디버깅을 쉽게 수행 하려면 소스 맵이 포함 되어 있습니다.
  * 성능에 대 한 클라이언트 쪽 코드를 최적화 하지 않습니다.
* **프로덕션**:
  * 소스 맵 제외합니다.
  * 묶음 및 축소를 통해 클라이언트 쪽 코드를 최적화합니다.

ASP.NET Core 라는 환경 변수를 사용 하 여 `ASPNETCORE_ENVIRONMENT` 구성 모드를 저장 합니다. 참조 **[환경을 설정할](xref:fundamentals/environments#set-the-environment)** 자세한 내용은 합니다.

### <a name="running-with-net-core-cli"></a>.NET Core CLI 사용 하 여 실행

프로젝트 루트에서 다음 명령을 실행 하 여 필요한 NuGet 및 npm 패키지를 복원 합니다.

```console
dotnet restore && npm i
```

빌드 및 응용 프로그램을 실행 합니다.

```console
dotnet run
```

Localhost에 따라 응용 프로그램을 시작 합니다 [런타임 구성 모드](#runtime-config-mode)합니다. 이동할 `http://localhost:5000` 브라우저에서 방문 페이지를 표시 합니다.

### <a name="running-with-visual-studio-2017"></a>Visual Studio 2017을 사용 하 여 실행

열기는 *.csproj* 에서 생성 된 파일을 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령입니다. 프로젝트를 열고 시 필요한 NuGet 및 npm 패키지를 자동으로 복원 됩니다. 이 복원 프로세스는 몇 분 정도 걸릴 수 있습니다 하 고 응용 프로그램은 작업이 완료 될 때 실행 하도록 준비 합니다. 누르거나 녹색 실행된 단추를 클릭 `Ctrl + F5`, 브라우저 응용 프로그램의 방문 페이지를 엽니다. Localhost에 따라 응용 프로그램을 실행 합니다 [런타임 구성 모드](#runtime-config-mode)합니다.

<a name="app-testing"></a>

## <a name="testing-the-app"></a>앱 테스트

SpaServices 템플릿은 사용 하 여 클라이언트 쪽 테스트를 실행 하도록 미리 구성 [Karma](https://karma-runner.github.io/1.0/index.html) 하 고 [Jasmine](https://jasmine.github.io/)합니다. Karma test runner를 해당 테스트는 jasmine는 JavaScript에 대 한 테스트 프레임 워크 인기 있는 단위. Karma과 작동 하도록 구성 되는 [Webpack 개발 미들웨어](#webpack-dev-middleware) 는 개발자 중지 될 때마다 변경 내용이 테스트를 실행 하는 데 필요한 되지 않습니다. 테스트 사례 또는 테스트 사례 자체에 대해 실행 되는 코드 인지 자동 테스트 실행 됩니다.

Angular 응용 프로그램을 사용 하 여 예를 들어, Jasmine 두 개의 테스트 사례는 아직 제공 합니다 `CounterComponent` 에 *counter.component.spec.ts* 파일:

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]

명령 프롬프트를 열고 합니다 *ClientApp* 디렉터리입니다. 다음 명령을 실행합니다.

```console
npm test
```

스크립트에 정의 된 설정을 읽어 Karma test runner를 시작 합니다 *karma.conf.js* 파일입니다. 기타 설정 합니다 *karma.conf.js* 식별을 통해 실행할 테스트 파일을 해당 `files` 배열:

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]

<a name="app-publishing"></a>

## <a name="publishing-the-application"></a>응용 프로그램 게시

배포 준비 패키지로 생성 된 클라이언트 쪽 자산 및 게시 된 ASP.NET Core 아티팩트를 결합 하는 것은 복잡할 수 있습니다. SpaServices 라는 사용자 지정 MSBuild 대상을 사용 하 여 전체 게시 프로세스를 오케스트레이션 하는 다행 스럽게도 `RunWebpack`:

[!code-xml[](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]

MSBuild 대상에는 다음 책임이 있습니다.

1. Npm 패키지를 복원 합니다.
1. 제 3 자, 클라이언트 쪽 자산 프로덕션 급 빌드 만들기
1. 프로덕션 급 빌드 사용자 지정 클라이언트 쪽 자산 만들기
1. Webpack에서 생성 된 자산을 게시 폴더에 복사

MSBuild 대상 실행 하는 경우 호출 됩니다.

```console
dotnet publish -c Release
```

## <a name="additional-resources"></a>추가 자료

* [Angular Docs](https://angular.io/docs)
