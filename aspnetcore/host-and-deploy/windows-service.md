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
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="ed16d-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="ed16d-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="ed16d-104">작성자: [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ed16d-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="ed16d-105">IIS를 사용 하 여 실행 하는 것 하지 않고 Windows에서 ASP.NET Core 응용 프로그램을 호스트 하는 권장된 방법은 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="ed16d-106">응용 프로그램 자동으로 수행할 수는 Windows 서비스로 호스트 되는 경우 시작 후 다시 부팅 되 고 사용자의 개입 없이 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="ed16d-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="ed16d-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="ed16d-108">에 대 한 샘플 응용 프로그램을 실행 하는 방법 참조 샘플의 *README.md* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-108">For instructions on how to run the sample app, see the sample's *README.md* file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed16d-109">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ed16d-109">Prerequisites</span></span>

* <span data-ttu-id="ed16d-110">앱을.NET Framework 런타임에 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-110">The app must run on the .NET Framework runtime.</span></span> <span data-ttu-id="ed16d-111">에 *.csproj* 파일,이 대 한 적절 한 값을 지정 [TargetFramework](/nuget/schema/target-frameworks) 및 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-111">In the *.csproj* file, specify appropriate values for [TargetFramework](/nuget/schema/target-frameworks) and [RuntimeIdentifier](/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="ed16d-112">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="ed16d-113">Visual Studio에서 프로젝트를 만들 때 사용 된 **ASP.NET Core 응용 프로그램 (.NET Framework)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="ed16d-114">사용 해야 합니다 (뿐 아니라 내부 네트워크)에서 인터넷을 통해 요청을 수신 하는 응용 프로그램을 하는 경우는 [HTTP.sys](xref:fundamentals/servers/httpsys) 웹 서버 (이전의 [WebListener](xref:fundamentals/servers/weblistener) ASP.NET Core 1.x 앱에 대 한) 대신[Kestrel](xref:fundamentals/servers/kestrel)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-114">If the app receives requests from the Internet (not just from an internal network), it must use the [HTTP.sys](xref:fundamentals/servers/httpsys) web server (formerly known as [WebListener](xref:fundamentals/servers/weblistener) for ASP.NET Core 1.x apps) rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="ed16d-115">IIS는 가장자리 배포에 Kestrel와 역방향 프록시 서버로 사용 하기 위한 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-115">IIS is recommended for use as a reverse proxy server with Kestrel for edge deployments.</span></span> <span data-ttu-id="ed16d-116">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed16d-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="get-started"></a><span data-ttu-id="ed16d-117">시작</span><span class="sxs-lookup"><span data-stu-id="ed16d-117">Get started</span></span>

<span data-ttu-id="ed16d-118">이 섹션에서는 서비스에서 실행 되도록 기존 ASP.NET Core 프로젝트를 설정 하는 데 필요한 최소한의 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

1. <span data-ttu-id="ed16d-119">NuGet 패키지 설치 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

2. <span data-ttu-id="ed16d-120">다음과 같이 변경 `Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="ed16d-120">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="ed16d-121">호출 `host.RunAsService` 대신 `host.Run`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-121">Call `host.RunAsService` instead of `host.Run`.</span></span>

   * <span data-ttu-id="ed16d-122">코드에서 호출 하는 경우 `UseContentRoot`, 경로 아닌 게시 위치를 사용 하 여 `Directory.GetCurrentDirectory()`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`.</span></span>

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ed16d-123">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ed16d-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   * * *

3. <span data-ttu-id="ed16d-125">폴더에 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-125">Publish the app to a folder.</span></span> <span data-ttu-id="ed16d-126">사용 하 여 [dotnet 게시](/dotnet/articles/core/tools/dotnet-publish) 또는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 폴더에 게시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-126">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

4. <span data-ttu-id="ed16d-127">만들고 서비스를 시작 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-127">Test by creating and starting the service.</span></span>

   <span data-ttu-id="ed16d-128">사용 하려면 관리자 권한으로 명령 셸을 열고는 [sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 만들고 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-128">Open a command shell with administrative privileges to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span> <span data-ttu-id="ed16d-129">MyService 서비스에 이름이 인 경우에 게시 `c:\svc`, 되며 AspNetCoreService 명명 된, 명령:</span><span class="sxs-lookup"><span data-stu-id="ed16d-129">If the service is named MyService, published to `c:\svc`, and named AspNetCoreService, the commands are:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   <span data-ttu-id="ed16d-130">`binPath` 값은 실행 파일 이름을 포함 하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-130">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span>

   ![콘솔 창에서 만들고 시작 예제](windows-service/_static/create-start.png)

   <span data-ttu-id="ed16d-132">콘솔 응용 프로그램으로 실행할 때 이러한 명령을 완료 하는 경우와 같은 경로을 찾습니다 (기본적으로 `http://localhost:5000`):</span><span class="sxs-lookup"><span data-stu-id="ed16d-132">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`):</span></span>

   ![서비스에서 실행](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="ed16d-134">서비스 외부에서 실행 하는 방법을 제공합니다</span><span class="sxs-lookup"><span data-stu-id="ed16d-134">Provide a way to run outside of a service</span></span>

<span data-ttu-id="ed16d-135">테스트 하 고 호출 하는 코드를 추가 하는 일반적인 것 이므로 외부 서비스를 실행 하는 경우 디버깅할 쉽게 `RunAsService` 특정 조건 에서만.</span><span class="sxs-lookup"><span data-stu-id="ed16d-135">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="ed16d-136">예를 들어, 응용 프로그램으로 콘솔 응용 프로그램으로 실행할 수는 `--console` 명령줄 인수나는 디버거가 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-136">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ed16d-137">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-137">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ed16d-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

* * *
## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="ed16d-139">중지 및 시작 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-139">Handle stopping and starting events</span></span>

<span data-ttu-id="ed16d-140">처리 하기 `OnStarting`, `OnStarted`, 및 `OnStopping` 이벤트를 다음과 같이 변경 추가:</span><span class="sxs-lookup"><span data-stu-id="ed16d-140">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

1. <span data-ttu-id="ed16d-141">파생 되는 클래스를 만듭니다 `WebHostService`:</span><span class="sxs-lookup"><span data-stu-id="ed16d-141">Create a class that derives from `WebHostService`:</span></span>

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="ed16d-142">에 대 한 확장 메서드를 만들어 `IWebHost` 사용자 지정을 통과 하 `WebHostService` 를 `ServiceBase.Run`:</span><span class="sxs-lookup"><span data-stu-id="ed16d-142">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`:</span></span>

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="ed16d-143">`Program.Main`, 새 확장 메서드를 호출 `RunAsCustomService`, 대신 `RunAsService`:</span><span class="sxs-lookup"><span data-stu-id="ed16d-143">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of `RunAsService`:</span></span>

   #### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ed16d-144">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-144">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   #### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ed16d-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ed16d-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   * * *
<span data-ttu-id="ed16d-146">하는 경우 사용자 지정 `WebHostService` 코드 (예:로 거) 종속성 주입에서 서비스를 실행 하려면에서 가져올는 `Services` 속성 `IWebHost`:</span><span class="sxs-lookup"><span data-stu-id="ed16d-146">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the `Services` property of `IWebHost`:</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="ed16d-147">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="ed16d-147">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="ed16d-148">서비스는 인터넷 이나 회사 네트워크의 요청과 상호 작용 하 고 프록시 뒤 또는 부하 분산 장치를 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-148">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="ed16d-149">자세한 내용은 참조 [프록시 서버를 사용 하 고 부하 분산 장치를 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-149">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="ed16d-150">감사의 글</span><span class="sxs-lookup"><span data-stu-id="ed16d-150">Acknowledgments</span></span>

<span data-ttu-id="ed16d-151">게시 된 원본의 도움을 받아이 문서의 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed16d-151">This article was written with the help of published sources:</span></span>

* [<span data-ttu-id="ed16d-152">ASP.NET Core Windows 서비스 호스팅</span><span class="sxs-lookup"><span data-stu-id="ed16d-152">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="ed16d-153">Windows 서비스에서 ASP.NET Core 프로그램을 호스트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ed16d-153">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
