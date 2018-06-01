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
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="60308-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="60308-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="60308-104">작성자: [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="60308-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="60308-105">IIS를 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트하는 권장 방법은 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 앱을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60308-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="60308-106">Windows 서비스로 호스트된 앱은 사용자 개입 없이 앱이 다시 부팅되거나 크래시된 후에 자동으로 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="60308-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="60308-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="60308-108">샘플 앱을 실행하는 방법에 대한 자세한 내용은 샘플의 *README.md* 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60308-108">For instructions on how to run the sample app, see the sample's *README.md* file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60308-109">전제 조건</span><span class="sxs-lookup"><span data-stu-id="60308-109">Prerequisites</span></span>

* <span data-ttu-id="60308-110">앱은 .NET Framework 런타임에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-110">The app must run on the .NET Framework runtime.</span></span> <span data-ttu-id="60308-111">*.csproj* 파일에서 [TargetFramework](/nuget/schema/target-frameworks) 및 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog)에 대한 적절한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-111">In the *.csproj* file, specify appropriate values for [TargetFramework](/nuget/schema/target-frameworks) and [RuntimeIdentifier](/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="60308-112">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="60308-113">Visual Studio에서 프로젝트를 만들 경우 **ASP.NET Core 응용 프로그램(.NET Framework)** 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="60308-114">앱은 인터넷(내부 네트워크만이 아님)에서 요청을 수신할 때 [Kestrel](xref:fundamentals/servers/kestrel) 대신 [HTTP.sys](xref:fundamentals/servers/httpsys) 웹 서버(이전 ASP.NET Core 1.x 앱에 대한 [WebListener](xref:fundamentals/servers/weblistener))를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-114">If the app receives requests from the Internet (not just from an internal network), it must use the [HTTP.sys](xref:fundamentals/servers/httpsys) web server (formerly known as [WebListener](xref:fundamentals/servers/weblistener) for ASP.NET Core 1.x apps) rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="60308-115">IIS는 에지 배포를 위해 Kestrel과 함께 역방향 프록시 서버로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-115">IIS is recommended for use as a reverse proxy server with Kestrel for edge deployments.</span></span> <span data-ttu-id="60308-116">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60308-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="get-started"></a><span data-ttu-id="60308-117">시작</span><span class="sxs-lookup"><span data-stu-id="60308-117">Get started</span></span>

<span data-ttu-id="60308-118">이 섹션에서는 기존 ASP.NET Core 프로젝트를 서비스에서 실행하도록 설정하는 데 필요한 최소 변경 내용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

1. <span data-ttu-id="60308-119">NuGet 패키지 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

2. <span data-ttu-id="60308-120">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-120">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="60308-121">`host.Run` 대신 `host.RunAsService`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-121">Call `host.RunAsService` instead of `host.Run`.</span></span>

   * <span data-ttu-id="60308-122">코드가 `UseContentRoot`를 호출하는 경우 `Directory.GetCurrentDirectory()` 대신 게시 위치의 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`.</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="60308-123">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="60308-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="60308-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="60308-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   ---

3. <span data-ttu-id="60308-125">앱을 폴더에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-125">Publish the app to a folder.</span></span> <span data-ttu-id="60308-126">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 또는 폴더에 게시되는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-126">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

4. <span data-ttu-id="60308-127">서비스를 만들고 시작해서 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-127">Test by creating and starting the service.</span></span>

   <span data-ttu-id="60308-128">관리자 권한으로 명령 셸을 열고 [sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-128">Open a command shell with administrative privileges to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span> <span data-ttu-id="60308-129">서비스가 MyService로 이름이 지정되고, `c:\svc`에 게시되고, AspNetCoreService로 이름이 지정되는 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-129">If the service is named MyService, published to `c:\svc`, and named AspNetCoreService, the commands are:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   <span data-ttu-id="60308-130">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="60308-130">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span>

   ![콘솔 창에서 예제를 만들고 시작](windows-service/_static/create-start.png)

   <span data-ttu-id="60308-132">이러한 명령이 완료되면 콘솔 앱으로 실행할 때와 동일한 경로로 이동합니다(기본적으로 `http://localhost:5000`).</span><span class="sxs-lookup"><span data-stu-id="60308-132">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`):</span></span>

   ![서비스로 실행](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="60308-134">서비스 외부에서 실행할 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-134">Provide a way to run outside of a service</span></span>

<span data-ttu-id="60308-135">서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-135">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="60308-136">예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-136">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="60308-137">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="60308-137">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="60308-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="60308-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

---

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="60308-139">이벤트 중지 및 시작 처리</span><span class="sxs-lookup"><span data-stu-id="60308-139">Handle stopping and starting events</span></span>

<span data-ttu-id="60308-140">`OnStarting`, `OnStarted` 및 `OnStopping` 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-140">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

1. <span data-ttu-id="60308-141">`WebHostService`에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60308-141">Create a class that derives from `WebHostService`:</span></span>

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="60308-142">사용자 지정 `WebHostService`를 `ServiceBase.Run`에 전달하는 `IWebHost`에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60308-142">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`:</span></span>

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="60308-143">`Program.Main`에서 `RunAsService` 대신 새 확장 메서드 `RunAsCustomService`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-143">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of `RunAsService`:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="60308-144">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="60308-144">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="60308-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="60308-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   ---

<span data-ttu-id="60308-146">사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 `IWebHost`의 `Services` 속성에서 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="60308-146">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the `Services` property of `IWebHost`:</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="60308-147">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="60308-147">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="60308-148">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60308-148">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="60308-149">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60308-149">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="60308-150">감사의 글</span><span class="sxs-lookup"><span data-stu-id="60308-150">Acknowledgments</span></span>

<span data-ttu-id="60308-151">이 문서는 게시된 소스를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60308-151">This article was written with the help of published sources:</span></span>

* [<span data-ttu-id="60308-152">Windows 서비스로 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="60308-152">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="60308-153">Windows 서비스에서 ASP.NET Core를 호스트하는 방법</span><span class="sxs-lookup"><span data-stu-id="60308-153">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
