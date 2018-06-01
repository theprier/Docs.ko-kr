---
title: Windows 서비스에서 ASP.NET Core 호스트
author: rick-anderson
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/windows-service
ms.openlocfilehash: 29f83ee585c73aeb57a09f70ea8e28650c05ce69
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
ms.locfileid: "34153531"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>Windows 서비스에서 ASP.NET Core 호스트

작성자: [Tom Dykstra](https://github.com/tdykstra)

IIS를 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트하는 권장 방법은 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 앱을 실행하는 것입니다. Windows 서비스로 호스트된 앱은 사용자 개입 없이 앱이 다시 부팅되거나 크래시된 후에 자동으로 시작될 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)). 샘플 앱을 실행하는 방법에 대한 자세한 내용은 샘플의 *README.md* 파일을 참조하세요.

## <a name="prerequisites"></a>전제 조건

* 앱은 .NET Framework 런타임에서 실행되어야 합니다. *.csproj* 파일에서 [TargetFramework](/nuget/schema/target-frameworks) 및 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog)에 대한 적절한 값을 지정합니다. 예를 들면 다음과 같습니다.

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  Visual Studio에서 프로젝트를 만들 경우 **ASP.NET Core 응용 프로그램(.NET Framework)** 템플릿을 사용합니다.

* 앱은 인터넷(내부 네트워크만이 아님)에서 요청을 수신할 때 [Kestrel](xref:fundamentals/servers/kestrel) 대신 [HTTP.sys](xref:fundamentals/servers/httpsys) 웹 서버(이전 ASP.NET Core 1.x 앱에 대한 [WebListener](xref:fundamentals/servers/weblistener))를 사용해야 합니다. IIS는 에지 배포를 위해 Kestrel과 함께 역방향 프록시 서버로 사용하는 것이 좋습니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

## <a name="get-started"></a>시작

이 섹션에서는 기존 ASP.NET Core 프로젝트를 서비스에서 실행하도록 설정하는 데 필요한 최소 변경 내용에 대해 설명합니다.

1. NuGet 패키지 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)를 설치합니다.

2. `Program.Main`에서 다음과 같이 변경합니다.

   * `host.Run` 대신 `host.RunAsService`를 호출합니다.

   * 코드가 `UseContentRoot`를 호출하는 경우 `Directory.GetCurrentDirectory()` 대신 게시 위치의 경로를 사용합니다.

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   ---

3. 앱을 폴더에 게시합니다. [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 또는 폴더에 게시되는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles)을 사용합니다.

4. 서비스를 만들고 시작해서 테스트합니다.

   관리자 권한으로 명령 셸을 열고 [sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만들고 시작합니다. 서비스가 MyService로 이름이 지정되고, `c:\svc`에 게시되고, AspNetCoreService로 이름이 지정되는 경우 명령은 다음과 같습니다.

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   `binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.

   ![콘솔 창에서 예제를 만들고 시작](windows-service/_static/create-start.png)

   이러한 명령이 완료되면 콘솔 앱으로 실행할 때와 동일한 경로로 이동합니다(기본적으로 `http://localhost:5000`).

   ![서비스로 실행](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a>서비스 외부에서 실행할 방법을 제공합니다.

서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다. 예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

---

## <a name="handle-stopping-and-starting-events"></a>이벤트 중지 및 시작 처리

`OnStarting`, `OnStarted` 및 `OnStopping` 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.

1. `WebHostService`에서 파생되는 클래스를 만듭니다.

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. 사용자 지정 `WebHostService`를 `ServiceBase.Run`에 전달하는 `IWebHost`에 대한 확장 메서드를 만듭니다.

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. `Program.Main`에서 `RunAsService` 대신 새 확장 메서드 `RunAsCustomService`를 호출합니다.

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   ---

사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 `IWebHost`의 `Services` 속성에서 서비스를 가져옵니다.

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

## <a name="acknowledgments"></a>감사의 글

이 문서는 게시된 소스를 사용하여 작성되었습니다.

* [Windows 서비스로 ASP.NET Core 호스트](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [Windows 서비스에서 ASP.NET Core를 호스트하는 방법](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
