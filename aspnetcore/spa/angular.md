---
title: ASP.NET Core와 함께 각 프로젝트 템플릿을 사용합니다
author: SteveSandersonMS
description: 각 및 각도 CLI에 대 한 ASP.NET Core 단일 페이지 응용 프로그램 (SPA) 프로젝트 템플릿으로 시작 하는 방법에 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/angular
ms.openlocfilehash: b4e48f40c3d4e3167e7fdb3534d2c33b3544592c
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="use-the-angular-project-template-with-aspnet-core"></a>ASP.NET Core와 함께 각 프로젝트 템플릿을 사용합니다

> [!NOTE]
> 이 설명서 포함 되지 않습니다 각도 프로젝트 템플릿에 대 한 ASP.NET 코어 2.0. 최신 각도 서식 파일을 수동으로 업데이트할 수 있습니다. 서식 파일은 기본적으로 ASP.NET Core 2.1에 포함 됩니다.

업데이트 된 각 프로젝트 템플릿은 있는 편리 하 게 시작 지점을 제공 ASP.NET Core에 대 한 각 및 각도 CLI를 사용 하는 다양 하 고 클라이언트 쪽 UI (사용자 인터페이스)를 구현 하는 앱입니다.

템플릿에 API 백 엔드 역할을 하는 ASP.NET Core 프로젝트 및는 각도 CLI 프로젝트의 역할을 하는 UI를 만드는 것과 같습니다. 서식 파일은 단일 응용 프로그램 프로젝트의 두 프로젝트 형식 호스팅의 편의 제공 합니다. 따라서 응용 프로그램 프로젝트 빌드 및 단일 단위로 게시 수입니다.

## <a name="create-a-new-app"></a>새 앱 만들기

ASP.NET Core 2.0을 사용 하는 경우 확인 했습니다. [설치 된 업데이트 된 각 프로젝트 템플릿](xref:spa/index#installation)합니다. ASP.NET Core 2.1 있을 경우 설치할 필요가 없습니다.

명령을 사용 하 여 명령 프롬프트에서 새 프로젝트 만들기 `dotnet new angular` 빈 디렉터리에 있습니다. 예를 들어 다음 명령에서 응용 프로그램을 만듭니다는 *내-새-app* 디렉터리와 해당 디렉터리에 스위치:

```console
dotnet new angular -o my-new-app
cd my-new-app
```

Visual Studio 또는.NET Core CLI에서 응용 프로그램을 실행 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

생성 된 열고 *.csproj* 파일, 및 여기에서 응용 프로그램 정상적으로 실행 합니다.

빌드 프로세스는 몇 분 정도 걸릴 수 있는 첫 번째 실행 시 npm 종속성을 복원 합니다. 후속 빌드는 훨씬 빠릅니다.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli/)

라는 환경 변수 해야 `ASPNETCORE_Environment` 값 `Development`합니다. (비 PowerShell 프롬프트)의 Windows에서는 실행 `SET ASPNETCORE_Environment=Development`합니다. Linux 또는 macOS 실행 `export ASPNETCORE_Environment=Development`합니다.

실행 [dotnet 빌드](/dotnet/core/tools/dotnet-build) 응용 프로그램을 확인 하기 올바르게를 작성 합니다. 첫 번째 실행에서 빌드 프로세스 몇 분 정도 걸릴 수 있는 npm 종속성을 복원 합니다. 후속 빌드는 훨씬 빠릅니다.

실행 [실행 dotnet](/dotnet/core/tools/dotnet-run) 앱을 시작 합니다. 다음과 비슷한 메시지가 기록 됩니다.

```console
Now listening on: http://localhost:<port>
```

브라우저에서이 URL로 이동 합니다.

응용 프로그램의 백그라운드에서 각도 CLI 서버 인스턴스를 시작 합니다. 다음과 비슷한 메시지가 기록 됩니다: <em>NG 라이브 개발 서버가 수신 하는 localhost:&lt;otherport&gt;에서 브라우저를 열고 http://localhost:&lt; otherport&gt; /</em>  . 이 메시지는 무시&mdash;있기 <strong>하지</strong> 결합 된 각도 CLI 및 ASP.NET Core 응용 프로그램에 대 한 URL입니다.

---

프로젝트 템플릿은 각도 응용 프로그램 및 ASP.NET Core 응용 프로그램을 만듭니다. ASP.NET Core 응용 프로그램은 데이터 액세스, 권한 부여 및 기타 서버 쪽 고려 사항에 대해 사용 하는 데 사용 됩니다. 에 있는 각 응용 프로그램의 *ClientApp* 하위 디렉터리를은 모든 UI 문제에 대 한 사용 하려고 합니다.

## <a name="add-pages-images-styles-modules-etc"></a>페이지, 이미지, 스타일, 모듈 등을 추가 합니다.

*ClientApp* 표준 각도 CLI 앱을 포함 하는 디렉터리입니다. 공식 참조 [각도 설명서](https://github.com/angular/angular-cli/wiki) 자세한 정보에 대 한 합니다.

이 템플릿으로 만든 각도 앱과 자체 각도 CLI를 통해 만든 간에 약간의 차이가 있습니다 (통해 `ng new`); 그러나 응용 프로그램의 기능 변경 되지 않습니다. 템플릿에서 만든 앱에 포함 되어는 [부트스트랩](https://getbootstrap.com/)-레이아웃 및 기본 라우팅 예제를 기반으로 합니다.

## <a name="run-ng-commands"></a>Ng 명령 실행

명령 프롬프트에서 전환 하는 *ClientApp* 하위 디렉터리:

```console
cd ClientApp
```

있는 경우는 `ng` 전역으로 설치 하는 도구를 실행할 수 있습니다 해당 명령 중 하나입니다. 예를 들어 실행할 수 있습니다 `ng lint`, `ng test`, 또는 다른 [각도 CLI 명령을](https://github.com/angular/angular-cli/wiki#additional-commands)합니다. 실행할 필요가 없는 `ng serve` 하지만 ASP.NET Core 응용 프로그램 처리 응용 프로그램의 서버 쪽 및 클라이언트 쪽 모두 부분을 처리 하기 때문에 있습니다. 사용 하 여 내부적으로 `ng serve` 개발에서 합니다.

없는 경우는 `ng` 도구 설치 됨, 실행 `npm run ng` 대신 합니다. 예를 들어 실행할 수 있습니다 `npm run ng lint` 또는 `npm run ng test`합니다.

## <a name="install-npm-packages"></a>npm 패키지 설치

제 3 자 npm 패키지를 설치 하려면 명령 프롬프트를 사용 하 여는 *ClientApp* 하위 디렉터리입니다. 예를 들어:

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a>게시 및 배포

개발, 응용 프로그램 개발자 편의 위해 최적화 된 모드에서 실행 됩니다. 예를 들어 JavaScript 번들 (있도록를 디버깅할 때 원래 TypeScript 코드를 볼 수 있습니다) 소스 맵이 포함 됩니다. 응용 프로그램 디스크에서 TypeScript, HTML 및 CSS 파일 변경 내용을 감시 하 고 자동으로 다시 컴파일 수 하 고이 변경 하 이러한 파일을 발견 시 다시 로드 하는 만듭니다.

프로덕션으로 성능에 최적화 된 응용 프로그램의 버전을 제공 합니다. 자동으로 실행 되도록 구성 됩니다. 게시 하면 빌드 구성을 내보냅니다는 축소 된, 미리 시간 (AoT) 컴파일된 클라이언트 쪽 코드의 빌드입니다. 개발 빌드 달리 프로덕션 빌드 서버에 설치 되는 Node.js 필요 하지 않습니다 (활성화 하지 않은 경우 [서버 쪽 사전 렌더링이](#server-side-rendering)).

사용할 수 [ASP.NET Core 호스팅 및 배포 방법](xref:host-and-deploy/index)합니다.

## <a name="run-ng-serve-independently"></a>"Ng serve"를 독립적으로 실행

프로젝트 개발 모드에서 ASP.NET Core 응용 프로그램이 시작 하는 경우 백그라운드에서 각도 CLI 서버의 자체 인스턴스를 시작 하도록 구성 됩니다. 별도 서버를 수동으로 실행할 수 없기 때문에 유용 합니다.

이 기본 설정에는 단점이 있습니다. C# 코드와 응용 프로그램을 다시 시작 해야 하는 경우 ASP.NET 핵심을 수정할 때마다 각도 CLI 서버 다시 시작 합니다. 약 10 초를 다시 시작 하려면 필요 합니다. 자주 C# 코드 편집 작업을 수행 하는 각도 CLI를 다시 시작 될 때까지 기다리는 하지 않으려는 경우 각도 CLI 서버 외부에서 ASP.NET Core 프로세스와 독립적으로 실행 합니다. 이렇게 하려면

1. 명령 프롬프트에서 전환 하는 *ClientApp* 하위 디렉터리 및 시작 각도 CLI 개발 서버:

    ```console
    cd ClientApp
    npm start
    ```

    > [!IMPORTANT]
    > 사용 하 여 `npm start` 하지 각도 CLI 개발 서버를 시작 하려면 `ng serve`되도록 구성에 *package.json* 가 적용 합니다. 관련 추가 각도 CLI 서버에 추가 매개 변수를 전달 하려면 `scripts` 줄 프로그램 *package.json* 파일입니다.

2. 자체 중 하나를 실행 하는 대신 외부 각도 CLI 인스턴스를 사용 하려면 ASP.NET Core 응용 프로그램을 수정 합니다. 사용자 *시작* 클래스, 대체는 `spa.UseAngularCliServer` 다음으로 호출 합니다.

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:4200");
    ```

ASP.NET Core 응용 프로그램을 시작 하면 각 CLI 서버를 시작 하지 않습니다. 수동으로 시작 된 인스턴스가 대신 사용 됩니다. 이 통해 시작 하 고 더 빠르게 다시 시작 합니다. 클라이언트 앱 될 때마다 다시 작성 하는 각도 CLI에 대 한 대기 중 더 이상입니다.

## <a name="server-side-rendering"></a>서버 쪽 렌더링

성능 기능으로, 클라이언트에서 실행할 뿐 아니라 서버에서 각 앱을 미리 렌더링을 선택할 수 있습니다. 이 경우에 브라우저 때문에 다운로드 하 고 JavaScript 번들을 실행 하기 전에 표시 될 응용 프로그램의 초기 UI를 나타내는 HTML 태그를 수신 하는 합니다. 대부분이 구성의 호출 하는 각 기능에서 제공 [각도 유니버설](https://universal.angular.io/)합니다.

> [!TIP]
> 서버 쪽 렌더링을 사용 하도록 설정 (SSR) 많은 개발 및 배포 하는 동안 추가 문제가 모두를 소개 합니다. 읽기 [SSR의 단점](#drawbacks-of-ssr) SSR 요구 사항에 가장 잘 맞는 인지 확인 하려면.

SSR를 사용 하도록 설정 하려면 프로젝트에 추가 된 횟수를 해야 합니다.

에 *시작* 클래스 *후* 를 구성 하는 줄 `spa.Options.SourcePath`, 및 *하기 전에* 호출 `UseAngularCliServer` 또는 `UseProxyToSpaDevelopmentServer`, 다음 추가:

[!code-csharp[](sample/AngularServerSideRendering/Startup.cs?name=snippet_Call_UseSpa&highlight=5-12)]

개발 모드에서이 코드는 스크립트를 실행 하 여 SSR 번들 작성 하려고 `build:ssr`에 정의 된 *ClientApp\package.json*합니다. 각 앱 작성이 `ssr`, 아직 정의 되지 않은 합니다. 

끝에는 `apps` 배열로 *ClientApp/.angular-cli.json*, 이름을 사용 하 여 추가 앱 정의 `ssr`합니다. 다음 옵션을 사용 합니다.

[!code-json[](sample/AngularServerSideRendering/ClientApp/.angular-cli.json?range=24-41)]

이 새 SSR 사용이 가능한 앱 구성에는 두 개의 추가 파일이 필요: *tsconfig.server.json* 및 *main.server.ts*합니다. *tsconfig.server.json* 파일 TypeScript 컴파일 옵션을 지정 합니다. *main.server.ts* 파일 SSR 하는 동안 코드 진입점으로 사용 합니다.

라는 새 파일을 추가 *tsconfig.server.json* 내 *ClientApp/src* (기존 함께 *tsconfig.app.json*), 다음을 포함 하 합니다.

[!code-json[](sample/AngularServerSideRendering/ClientApp/src/tsconfig.server.json)]

이 파일의 각 AoT 컴파일러를 호출 하는 모듈을 찾도록 구성 `app.server.module`합니다. 에 새 파일을 만들어이 추가할 *ClientApp/src/app/app.server.module.ts* (기존 함께 *app.module.ts*) 다음 포함 된: 

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/app/app.server.module.ts)]

클라이언트 쪽에서이 모듈 상속 `app.module` SSR 하는 동안 사용할 수 있는 추가 Angular 모듈을 정의 하 고 있습니다.

이전에 설명한 대로 새 `ssr` 항목 *.angular cli.json* 라는 항목 지점 파일로 참조 *main.server.ts*합니다. 해당 파일을 아직 추가 하지 않은 하 고 수행 됩니다. 에 새 파일을 만들 *ClientApp/src/main.server.ts* (기존 함께 *main.ts*), 다음을 포함 하 합니다.

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/main.server.ts)]

이 파일의이 코드를 실행할 때의 ASP.NET Core를 실행 각 요청에 대 한는 `UseSpaPrerendering` 에 추가 하는 미들웨어는 *시작* 클래스입니다. 수신 다루는 `params` (예: URL 요청 되 고),.NET 코드 및 결과 HTML을 가져올 각도 SSR Api를 호출 합니다. 

엄격 하 게-말하기, 이것이 SSR 개발 모드에서 사용 하도록 설정 하는 데 충분 합니다. 게시 된 경우 앱이 제대로 작동 되도록 한 마지막 변경 하는 것이 반드시 합니다. 응용 프로그램의 main에서 *.csproj* 파일에서 설정 된 `BuildServerSideRenderer` 속성 값을 `true`:

[!code-xml[](sample/AngularServerSideRendering/AngularServerSideRendering.csproj?name=snippet_EnableBuildServerSideRenderer)]

이렇게 하면 빌드 프로세스가 실행 되도록 구성 `build:ssr` 게시 하는 동안 SSR 파일 서버에 배포 합니다. 이 사용 하지 않을 경우, 프로덕션 환경에서 SSR 실패 합니다.

응용 프로그램 개발 또는 프로덕션 모드에서 실행 되 면 각도 코드가 미리 렌더링 되는 HTML로 서버에 있습니다. 클라이언트 쪽 코드를 정상적으로 실행합니다.

### <a name="pass-data-from-net-code-into-typescript-code"></a>TypeScript 코드를.NET 코드에서 데이터 전달

SSR, 하는 동안 각 앱에 ASP.NET Core 응용 프로그램에서 요청 데이터를 전달 하는 것이 좋습니다. 예를 들어 쿠키 정보를 전달할 수 또는 데이터베이스에서 읽는 것입니다. 이 작업을 수행 하려면 편집 하 여 *시작* 클래스입니다. 에 대 한 콜백을 `UseSpaPrerendering`에 대 한 값 설정 `options.SupplyData` 다음과 같은:

```csharp
options.SupplyData = (context, data) =>
{
    // Creates a new value called isHttpsRequest that's passed to TypeScript code
    data["isHttpsRequest"] = context.Request.IsHttps;
};
```

`SupplyData` 전달 임의의 콜백 수, 요청, (문자열, 부울 또는 숫자)에 JSON 직렬화 가능한 데이터입니다. 프로그램 *main.server.ts* 관리 코드를 수신으로 `params.data`합니다. 위의 코드 예제는 부울 값으로 전달 하는 예를 들어 `params.data.isHttpsRequest` 에 `createServerRenderer` 콜백 합니다. 각에서 지 원하는 어떤 방식으로든 응용 프로그램의 다른 부분에이 값을 전달할 수 있습니다. 예를 들어 참조 방법을 *main.server.ts* 전달는 `BASE_URL` 값의 생성자는 받기 위해 선언 된 모든 구성 요소입니다.

### <a name="drawbacks-of-ssr"></a>SSR의 단점

일부 앱 SSR에서 활용합니다. 주요 이점은 성능을 인식 됩니다. 느린 네트워크 연결을 통해 또는 느린 모바일 장치에 응용 프로그램에 도달 하는 방문자까지 약간의 시간이 데이터를 가져오거나 JavaScript 번들을 구문 분석 하는 경우에 초기 UI 신속 하 게 참조 합니다. 그러나 많은 SPAs는 주로 빠른 컴퓨터 신속 하 고 내부 회사 네트워크를 통해 응용 프로그램이 거의 즉시 표시 됩니다.

이와 동시에는 SSR를 사용 하도록 설정 하는 중요 한 단점이 있습니다. 개발 프로세스에 복잡성을 추가합니다. 코드는 두 개의 서로 다른 환경에서 실행 해야 합니다: 클라이언트 및 서버 쪽은 Node.js 환경에서 ASP.NET Core에서 호출 합니다. 기억해 야 할 일부의 원인 다음과 같습니다.

* SSR은 프로덕션 서버에서 Node.js 설치 되어 있어야 합니다. Azure 앱 서비스 등의 일부 배포 시나리오에 대 한 있지만 대 한 Azure 서비스 패브릭 등의 다른 경우 자동으로 됩니다.
* 사용 하도록 설정는 `BuildServerSideRenderer` 플래그 원인 빌드 프로그램 *node_modules* 게시 하는 디렉터리입니다. 이 폴더에 20, 000 명 파일이 배포 시간을 향상 시킵니다.
* Node.js 환경에서 코드를 실행 하려면이를 사용할 수 없게 브라우저의 JavaScript Api의 존재 여부와 같은 `window` 또는 `localStorage`합니다. 코드 (또는 일부 다른 공급 업체 라이브러리 참조)를 하 려 하면 이러한 Api를 사용 하 여 얻게 됩니다 오류가 SSR 중. 예를 들어 사용 하지 않는 jQuery 여러 위치에서 브라우저의 Api를 참조 하기 때문에 있습니다. 오류를 방지 하려면 SSR 것을 방지 하거나 브라우저 전용 Api 또는 라이브러리를 방지 해야 합니다. 위해 SSR 중에 호출 되지 않습니다 확인에 이러한 Api에 대 한 모든 호출을 래핑할 수 있습니다. 예를 들어 다음과 같은 확인을 사용 하 여 JavaScript 또는 TypeScript 코드에서:

    ```javascript
    if (typeof window !== 'undefined') {
        // Call browser-specific APIs here
    }
    ```
