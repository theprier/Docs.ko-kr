---
title: "다양한 환경에서 작업하기"
author: ardalis
description: "ASP.NET Core가 다양한 환경에서 응용 프로그램의 동작을 제어하기 위해 지원하는 기능들을 살펴봅니다."
keywords: "ASP.NET Core, 환경 설정, ASPNETCORE_ENVIRONMENT"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: b5bba985-be12-4464-9a01-df3599b2a6f1
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/environments
ms.openlocfilehash: 2a92c50085e70b4a505913c86348ba5fe54f6d13
ms.sourcegitcommit: 67811da1278c75cb10994602c13bd5adec3f0907
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2017
---
# <a name="working-with-multiple-environments"></a>다양한 환경에서 작업하기

작성자: [Steve Smith](https://ardalis.com/)

ASP.NET Core는 개발, 스테이징, 프로덕션 등의 다양한 환경에서 앱의 동작을 제어하기 위한 기능을 제공합니다. 환경 변수를 이용해서 런타임 환경을 지정하여 해당 환경에 적합하게 앱을 구성할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="development-staging-production"></a>개발, 스테이징, 프로덕션

ASP.NET Core는 응용 프로그램이 현재 실행되고 있는 환경을 구분하기 위해 `ASPNETCORE_ENVIRONMENT`라는 특정 환경 변수를 참조합니다. 이 변수는 원하는 어떤 값으로도 설정할 수 있지만, 대부분 관례에 따라 세 가지 값, `Development`, `Staging` 및 `Production` 중 한 가지가 사용됩니다. ASP.NET Core와 함께 제공되는 예제나 템플릿을 살펴보면 이 값들이 사용되고 있는 것을 확인할 수 있습니다.

프로그래밍 방식으로 응용 프로그램 내에서 현재 환경 설정을 감지할 수 있습니다. 또는 Environment [태그 도우미](../mvc/views/tag-helpers/index.md)를 사용해서 응용 프로그램의 현재 환경을 기반으로 [뷰](../mvc/views/index.md)에 특정 섹션을 포함시킬 수도 있습니다.

참고: Windows 및 macOS는 지정된 환경 이름의 대소문자를 구분하지 않습니다. 환경 변수를 `Development`나 `development` 또는 `DEVELOPMENT` 중 어떤 값으로 설정하더라도 그 결과는 동일합니다. 반면 Linux는 기본적으로 **대소문자를 구분**하는 OS입니다. 따라서 환경 변수, 파일명 그리고 설정에서 항상 대소문자를 구분해야 합니다.

### <a name="development"></a>개발

이 환경은 응용 프로그램을 개발할 때 사용되는 환경입니다. 일반적으로 응용 프로그램이 프로덕션 환경에서 실행될 때는 사용하지 않는 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page) 같은 기능을 활용하기 위한 목적으로 사용됩니다.

만약 Visual Studio를 사용하고 있다면, 프로젝트의 디버그 프로필에서 환경을 구성할 수 있습니다. 디버그 프로필에서는 응용 프로그램을 시작할 때 사용할 [서버](xref:fundamentals/servers/index)와 설정할 모든 환경 변수를 지정합니다. 한 프로젝트에 환경 변수를 서로 다르게 구성한 별개의 디버그 프로필이 다수 존재할 수 있습니다. 이 프로필들은 웹 응용 프로그램 프로젝트의 **속성** 메뉴의  **디버그** 탭을 통해서 관리됩니다. 프로젝트 속성에서 설정한 값은 *launchSettings.json* 파일에 저장되며, 이 파일을 직접 편집해서 프로필을 구성할 수도 있습니다.

다음은 IIS Express 프로필을 보여줍니다:

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

다음은 `Development` 환경과 `Staging` 환경을 위한 프로필을 포함하고 있는 `launchSettings.json` 파일을 보여줍니다:

[!code-json[Main](../fundamentals/environments/sample/src/Environments/Properties/launchSettings.json?highlight=15,22)]

프로젝트 프로필의 변경 사항은 사용되는 웹 서버가 재시작될 때까지 반영되지 않을 수도 있습니다 (특히, Kestrel은 재시작해야만 해당 환경의 변경 사항을 감지할 수 있습니다).

>[!WARNING]
> *launchSettings.json* 파일에 저장되는 환경 변수는 어떤 방식으로도 보호되지 않으며, 만약 소스 코드 리파지터리를 사용하고 있다면 프로젝트의 소스 코드와 함께 리파지터리에 저장됩니다. **따라서 이 파일에는 자격 증명이나 기타 보안에 민감한 데이터를 저장하면 안됩니다.** 만약 그런 데이터를 저장해야만 한다면 [개발 중 민감한 응용 프로그램 정보 안전하게 저장하기](../security/app-secrets.md#security-app-secrets)에서 설명하는 Secret Manager 도구를 사용하는 것이 좋습니다.

### <a name="staging"></a>스테이징

일반적으로 `Staging` 환경은 프로덕션에 배포하기 전, 마지막 테스트에 활용되는 사전 프로덕션 환경입니다. 이 환경의 물리적 특성은 운영 환경의 그것을 그대로 반영하므로, 이상적인 경우 운영 환경에서 발생할 수 있는 모든 문제점을 스테이징 환경에서 먼저 확인함으로써 사용자에게 영향을 주지 않고 문제점을 해결할 수 있습니다.

### <a name="production"></a>프로덕션

`Production` 환경은 응용 프로그램이 실제로 실행되고 최종 사용자에 의해 사용되는 환경입니다. 이 환경은 보안과 성능, 그리고 응용 프로그램의 견고성이 극대화되도록 구성되어야 합니다. 다음은 일반적으로 개발 환경과 프로덕션 환경 사이에 차이점이 존재하는 몇 가지 설정입니다:

* 캐싱 사용하기

* 모든 클라이언트 측 리소스가 번들 및 축소되고 있는지, 그리고 최대한 CDN을 통해서 서비스되고 있는지 확인하기

* 진단용 ErrorPages 중지하기

* 친숙한 오류 페이지 사용하기

* 프로덕션에 적합한 로깅 및 모니터링 사용하기 (예, [Application Insights](https://azure.microsoft.com/documentation/articles/app-insights-asp-net-five/))

이 목록은 단지 한 가지 사례일 뿐입니다. 그리고 응용 프로그램의 너무 많은 부분에서 환경 검사를 반복적으로 수행하지 않는 것이 좋습니다. 대신 가급적 `Startup` 클래스에서 환경 검사를 수행하는 방식을 권장합니다.

## <a name="setting-the-environment"></a>환경 설정하기

환경을 설정하는 방법은 운영 체제에 따라 달라집니다.

### <a name="windows"></a>Windows
응용 프로그램이 `dotnet run` 명령을 통해서 시작되는 경우, 현재 세션에 대해 `ASPNETCORE_ENVIRONMENT`를 설정하려면 다음 명령을 사용합니다.

**명령줄**
```
set ASPNETCORE_ENVIRONMENT=Development
```
**PowerShell**
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

그러나 이 명령은 오직 현재 창에 대해서만 적용됩니다. 따라서 창이 닫히면 `ASPNETCORE_ENVIRONMENT` 설정은 기본 설정 또는 시스템 값으로 되돌아갑니다. Windows에서 이 값을 전역으로 설정하려면 **제어판** > **시스템 및 보안** > **시스템** > **고급 시스템 설정**을 열고 `ASPNETCORE_ENVIRONMENT` 환경 변수 값을 추가하거나 편집합니다.

![시스템의 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET 코어 환경 변수](environments/_static/windows_aspnetcore_environment.png) 

**web.config**

[ASP.NET Core 모듈 구성 참조](xref:hosting/aspnet-core-module#setting-environment-variables) 주제의 *환경 변수 설정하기* 항목을 참고하시기 바랍니다.

**IIS 응용 프로그램 풀 별 환경 변수 설정**

격리된 응용 프로그램 풀에서 실행되는 (IIS 10.0 이상에서 지원됨) 개별 응용 프로그램에 대한 환경 변수를 설정해야 할 경우, IIS 참조 문서의 [\<environmentVariables> 환경 변수](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목 중, *AppCmd.exe 명령* 섹션을 참고하시기 바랍니다.

### <a name="macos"></a>MacOS
macOS의 경우, 응용 프로그램을 실행할 때 인라인으로 현재 환경을 설정할 수 있습니다.

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
또는, `export`를 이용해서 응용 프로그램을 실행하기 전에 미리 설정할 수도 있습니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
``` 
시스템 수준의 환경 변수는 *.bashrc* 또는 *.bash_profile* 파일에 설정됩니다. 텍스트 편집기로 파일을 편집해서 다음 명령문을 추가합니다.

```
export ASPNETCORE_ENVIRONMENT=Development
```  

### <a name="linux"></a>Linux
Linux 배포판의 경우, 세션 기반의 변수를 설정하려면 명령줄에서 `export` 명령을, 시스템 수준의 환경 변수를 설정하려면 *bash_profile* 파일을 사용합니다.

## <a name="determining-the-environment-at-runtime"></a>런타임에 환경 확인하기

`IHostingEnvironment` 서비스는 환경과 관련된 작업에 대한 핵심적인 추상화를 제공합니다. 이 서비스는 ASP.NET 호스팅 계층에서 제공되며, [종속성 주입](dependency-injection.md)을 통해서 시작 로직에 주입할 수 있습니다. Visual Studio의 ASP.NET Core 웹 사이트 템플릿에서는 이 방식을 활용해서 현재 환경에 해당하는 구성 파일을 로드하고 (구성 파일이 존재할 경우), 응용 프로그램의 오류 처리 설정을 사용자 지정합니다. 두 경우 모두, 적절한 방법으로 전달된 `IHostingEnvironment` 인스턴스의 `EnvironmentName`이나 `IsEnvironment`를 호출해서 현재 지정된 환경을 확인하는 방식으로 동작합니다.

> [!NOTE]
> 특정 환경에서 응용 프로그램이 실행 중인지 확인해야 할 경우, 단순히 `env.EnvironmentName == "Development"` 같이 문자열을 비교하는 대신, 안전하게 대소문자를 구분하지 않는 `env.IsEnvironment("environmentname")` 메서드를 사용하십시오.

예를 들어서, Configure 메서드에 다음과 같은 코드를 작성하면 환경별 오류 처리를 구성할 수 있습니다:

[!code-csharp[Main](environments/sample/src/Environments/Startup.cs?range=19-30)]

이 코드에서는 앱이 `Development` 환경에서 실행 중인 경우에만 Visual Studio의 "BrowserLink" 기능을 사용하기 위해 필요한 런타임 지원, 개발 환경 전용 오류 페이지 (일반적으로 이 기능은 프로덕션에서는 사용하지 않습니다) 및 데이터베이스 전용 오류 페이지가 (이 기능은 마이그레이션을 적용할 수 있는 기능을 제공하므로 개발 환경에서만 사용해야 합니다) 활성화됩니다. 반면, 앱이 개발 환경에서 실행 중이지 않을 경우, 처리되지 않은 모든 예외에 대한 응답으로 표준 오류 처리 페이지가 출력되도록 구성됩니다.

현재 환경에 따라서 런타임에 클라이언트로 전송할 콘텐츠를 결정해야 할 수도 있습니다. 가령, 개발 환경에서는 디버깅이 쉽도록 축소되지 않은 스크립트와 스타일 시트를 제공합니다. 반면 프로덕션 및 테스트 환경에서는 CDN을 이용해서 축소된 버전을 제공하는 경우가 대부분입니다. 이 작업은 Environment [태그 도우미](../mvc/views/tag-helpers/intro.md)로 처리할 수 있습니다. Environment 태그 도우미는 현재 환경이 `names` 어트리뷰트에 지정한 환경 중 하나와 일치하는 경우에만 그 내용을 렌더링합니다.

[!code-html[Main](environments/sample/src/Environments/Views/Shared/_Layout.cshtml?range=13-22)]

응용 프로그램에서 태그 도우미를 활용하려면 [태그 도우미 소개](../mvc/views/tag-helpers/intro.md)를 참고하시기 바랍니다.

## <a name="startup-conventions"></a>Startup 규약

ASP.NET Core는 현재 환경을 기반으로 응용 프로그램의 시작을 구성하는 규약 기반의 접근 방식을 지원합니다. 또한 응용 프로그램이 실행 중인 환경에 따라서 응용 프로그램이 동작하는 방식을 프로그래밍적인 방식으로 제어할 수 있으며, 자신만의 규약을 만들고 관리할 수 있습니다.

ASP.NET Core 응용 프로그램이 시작될 때, 응용 프로그램을 부트스트랩 하고 구성 설정을 로드하는 등의 작업에 `Startup` 클래스가 사용됩니다. ([ASP.NET 시작에 대해 자세히 알아보기](startup.md)). 그런데, 만약 `Startup{EnvironmentName}`라는 클래스가 존재하고 (예, `StartupDevelopment`), `ASPNETCORE_ENVIRONMENT` 환경 변수의 값이 이 이름과 일치하면 해당 클래스가 `Startup` 클래스 대신 사용됩니다. 따라서 이 기능을 활용하면 우선 개발 환경을 위한 `Startup` 클래스를 구성하고, 응용 프로그램이 프로덕션에서 실행될 때 사용될 별도의 `StartupProduction` 클래스를 구성할 수 있습니다. 물론 그 반대의 경우도 마찬가지입니다.

> [!NOTE]
> `WebHostBuilder.UseStartup<TStartup>()`를 호출하면 구성 섹션이 재정의됩니다.

또한 현재 환경을 기반으로 하는 완전히 별개의 Startup 클래스를 사용하는 대신, `Startup` 클래스 내부에서 자체적으로 응용 프로그램의 구성 방법을 제어할 수도 있습니다. `Configure()` 메서드와 `ConfigureServices()` 메서드 역시 `Startup` 클래스 자체와 비슷한 방식으로 `Configure{EnvironmentName}()` 및 `Configure{EnvironmentName}Services()` 형태의 환경 전용 버전 메서드를 지원합니다. 따라서 `ConfigureDevelopment()`라는 메서드를 정의할 경우, 개발 환경에서는 `Configure()` 대신 이 메서드가 호출됩니다. 마찬가지로 동일한 환경에서 `ConfigureServices()` 대신 `ConfigureDevelopmentServices()` 메서드가 호출됩니다.

## <a name="summary"></a>요약

ASP.NET Core는 개발자가 다양한 환경에서 응용 프로그램이 동작하는 방식을 손쉽게 제어할 수 있도록 다양한 기능과 규약을 제공합니다. 응용 프로그램을 개발에서 스테이징으로, 그리고 다시 프로덕션으로 게시할 때, 환경에 맞게 환경 변수를 적절히 설정하면 디버깅, 테스트 또는 프로덕션 용도에 맞게 응용 프로그램을 최적화시킬 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* [구성](configuration.md)

* [태그 도우미 소개](../mvc/views/tag-helpers/intro.md)
