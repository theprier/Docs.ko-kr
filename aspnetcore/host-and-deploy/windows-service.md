---
title: Windows 서비스에서 ASP.NET Core 호스트
author: tdykstra
description: Windows 서비스에서 ASP.NET Core 응용 프로그램을 호스트 하는 방법을 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/windows-service
ms.openlocfilehash: b0b27f274de1ca88b20bf582127132527b553ce0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="host-aspnet-core-in-a-windows-service"></a>Windows 서비스에서 ASP.NET Core 호스트

작성자: [Tom Dykstra](https://github.com/tdykstra)

IIS를 사용 하 여 실행 하는 것 하지 않고 Windows에서 ASP.NET Core 응용 프로그램을 호스트 하는 권장된 방법은 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)합니다. 응용 프로그램 자동으로 수행할 수는 Windows 서비스로 호스트 되는 경우 시작 후 다시 부팅 되 고 사용자의 개입 없이 충돌 합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)). 에 대 한 샘플 응용 프로그램을 실행 하는 방법 참조 샘플의 *README.md* 파일입니다.

## <a name="prerequisites"></a>전제 조건

* 앱을.NET Framework 런타임에 실행 해야 합니다. 에 *.csproj* 파일,이 대 한 적절 한 값을 지정 [TargetFramework](/nuget/schema/target-frameworks) 및 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog)합니다. 예를 들면 다음과 같습니다.

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  Visual Studio에서 프로젝트를 만들 때 사용 된 **ASP.NET Core 응용 프로그램 (.NET Framework)** 서식 파일입니다.

* 사용 해야 합니다 (뿐 아니라 내부 네트워크)에서 인터넷을 통해 요청을 수신 하는 응용 프로그램을 하는 경우는 [HTTP.sys](xref:fundamentals/servers/httpsys) 웹 서버 (이전의 [WebListener](xref:fundamentals/servers/weblistener) ASP.NET Core 1.x 앱에 대 한) 대신[Kestrel](xref:fundamentals/servers/kestrel)합니다. IIS는 가장자리 배포에 Kestrel와 역방향 프록시 서버로 사용 하기 위한 권장 됩니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

## <a name="get-started"></a>시작

이 섹션에서는 서비스에서 실행 되도록 기존 ASP.NET Core 프로젝트를 설정 하는 데 필요한 최소한의 내용을 설명 합니다.

1. NuGet 패키지 설치 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)합니다.

2. 다음과 같이 변경 `Program.Main`:

   * 호출 `host.RunAsService` 대신 `host.Run`합니다.

   * 코드에서 호출 하는 경우 `UseContentRoot`, 경로 아닌 게시 위치를 사용 하 여 `Directory.GetCurrentDirectory()`합니다.

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   * * *

3. 폴더에 앱을 게시 합니다. 사용 하 여 [dotnet 게시](/dotnet/articles/core/tools/dotnet-publish) 또는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 폴더에 게시 하는 합니다.

4. 만들고 서비스를 시작 하 여 테스트 합니다.

   사용 하려면 관리자 권한으로 명령 셸을 열고는 [sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 만들고 서비스를 시작 합니다. MyService 서비스에 이름이 인 경우에 게시 `c:\svc`, 되며 AspNetCoreService 명명 된, 명령:

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   `binPath` 값은 실행 파일 이름을 포함 하는 앱의 실행 파일 경로입니다.

   ![콘솔 창에서 만들고 시작 예제](windows-service/_static/create-start.png)

   콘솔 응용 프로그램으로 실행할 때 이러한 명령을 완료 하는 경우와 같은 경로을 찾습니다 (기본적으로 `http://localhost:5000`):

   ![서비스에서 실행](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a>서비스 외부에서 실행 하는 방법을 제공합니다

테스트 하 고 호출 하는 코드를 추가 하는 일반적인 것 이므로 외부 서비스를 실행 하는 경우 디버깅할 쉽게 `RunAsService` 특정 조건 에서만. 예를 들어, 응용 프로그램으로 콘솔 응용 프로그램으로 실행할 수는 `--console` 명령줄 인수나는 디버거가 연결 됩니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

* * *
## <a name="handle-stopping-and-starting-events"></a>중지 및 시작 이벤트를 처리 합니다.

처리 하기 `OnStarting`, `OnStarted`, 및 `OnStopping` 이벤트를 다음과 같이 변경 추가:

1. 파생 되는 클래스를 만듭니다 `WebHostService`:

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. 에 대 한 확장 메서드를 만들어 `IWebHost` 사용자 지정을 통과 하 `WebHostService` 를 `ServiceBase.Run`:

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. `Program.Main`, 새 확장 메서드를 호출 `RunAsCustomService`, 대신 `RunAsService`:

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   * * *
하는 경우 사용자 지정 `WebHostService` 코드 (예:로 거) 종속성 주입에서 서비스를 실행 하려면에서 가져올는 `Services` 속성 `IWebHost`:

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

서비스는 인터넷 이나 회사 네트워크의 요청과 상호 작용 하 고 프록시 뒤 또는 부하 분산 장치를 추가 구성이 필요할 수 있습니다. 자세한 내용은 참조 [프록시 서버를 사용 하 고 부하 분산 장치를 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)합니다.

## <a name="acknowledgments"></a>감사의 글

게시 된 원본의 도움을 받아이 문서의 작성 했습니다.

* [ASP.NET Core Windows 서비스 호스팅](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [Windows 서비스에서 ASP.NET Core 프로그램을 호스트 하는 방법](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
