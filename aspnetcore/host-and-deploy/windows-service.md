---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: e9e10b0bc99b2c54bf342121b1a454be5dac66c6
ms.sourcegitcommit: 661d30492d5ef7bbca4f7e709f40d8f3309d2dac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37938199"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="afb25-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="afb25-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="afb25-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="afb25-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="afb25-105">IIS를 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="afb25-106">Windows 서비스로 호스트된 앱은 사용자 개입 없이 앱이 다시 부팅되거나 크래시된 후에 자동으로 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="afb25-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="afb25-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="get-started"></a><span data-ttu-id="afb25-108">시작</span><span class="sxs-lookup"><span data-stu-id="afb25-108">Get started</span></span>

<span data-ttu-id="afb25-109">기존 ASP.NET Core 프로젝트를 서비스에서 실행하도록 설정하려면 다음과 같은 최소 변경 내용이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-109">The following minimum changes are required to set up an existing ASP.NET Core project to run in a service:</span></span>

1. <span data-ttu-id="afb25-110">프로젝트 파일에서:</span><span class="sxs-lookup"><span data-stu-id="afb25-110">In the project file:</span></span>

   1. <span data-ttu-id="afb25-111">런타임 식별자의 존재 여부를 확인하거나 이를 대상 프레임워크를 포함하는 **\<PropertyGroup>** 에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-111">Confirm the presence of the runtime identifier or add it to the **\<PropertyGroup>** that contains the target framework:</span></span>

      ::: moniker range=">= aspnetcore-2.1"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="= aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="< aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

   1. <span data-ttu-id="afb25-112">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-112">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

1. <span data-ttu-id="afb25-113">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-113">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="afb25-114">`host.Run` 대신 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-114">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="afb25-115">[UseContentRoot](xref:fundamentals/host/web-host#content-root)를 호출하여 `Directory.GetCurrentDirectory()` 대신 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-115">Call [UseContentRoot](xref:fundamentals/host/web-host#content-root) and use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     ::: moniker range=">= aspnetcore-2.0"

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,12)]

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]

     ::: moniker-end

1. <span data-ttu-id="afb25-116">앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-116">Publish the app.</span></span> <span data-ttu-id="afb25-117">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 또는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-117">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles).</span></span>

   <span data-ttu-id="afb25-118">명령줄에서 샘플 앱을 게시하려면 프로젝트 폴더의 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-118">To publish the sample app from the command line, run the following command in a console window from the project folder:</span></span>

   ```console
   dotnet publish --configuration Release
   ```

1. <span data-ttu-id="afb25-119">[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-119">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="afb25-120">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-120">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="afb25-121">**경로의 시작 부분에서 등호와 인용 문자 사이에 공간이 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="afb25-121">**The space between the equal sign and the quote character at the start of the path is required.**</span></span>

   ```console
   sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"
   ```

   <span data-ttu-id="afb25-122">프로젝트 폴더에서 게시된 서비스의 경우 *publish* 폴더에 대한 경로를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-122">For a service published in the project folder, use the path to the *publish* folder to create the service.</span></span> <span data-ttu-id="afb25-123">다음 예제에서 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-123">In the following example, the service is:</span></span>

   * <span data-ttu-id="afb25-124">**MyService**라는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-124">Named **MyService**.</span></span>
   * <span data-ttu-id="afb25-125">*c:\\my_services\\AspNetCoreService\\bin\\Release\\&lt;TARGET_FRAMEWORK&gt;\\publish* 폴더에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-125">Published to the *c:\\my_services\\AspNetCoreService\\bin\\Release\\&lt;TARGET_FRAMEWORK&gt;\\publish* folder.</span></span>
   * <span data-ttu-id="afb25-126">*AspNetCoreService.exe*라는 앱 실행 파일에서 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-126">Represented by an app executable named *AspNetCoreService.exe*.</span></span>

   <span data-ttu-id="afb25-127">관리자 권한으로 명령 셸을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-127">Open a command shell with administrative privileges and run the following command:</span></span>

   ```console
   sc create MyService binPath= "c:\my_services\AspNetCoreService\bin\Release\<TARGET_FRAMEWORK>\publish\AspNetCoreService.exe"
   ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="afb25-128">`binPath=` 인수와 해당 값 사이에 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-128">Make sure the space is present between the `binPath=` argument and its value.</span></span>
   
   <span data-ttu-id="afb25-129">다른 폴더의 서비스를 게시하고 시작하려면:</span><span class="sxs-lookup"><span data-stu-id="afb25-129">To publish and start the service from a different folder:</span></span>
   
   1. <span data-ttu-id="afb25-130">`dotnet publish` 명령에 대해 [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-130">Use the [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) option on the `dotnet publish` command.</span></span>
   1. <span data-ttu-id="afb25-131">출력 폴더 경로를 사용하는 `sc.exe` 명령으로 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-131">Create the service with the `sc.exe` command using the output folder path.</span></span> <span data-ttu-id="afb25-132">`binPath`에 제공된 경로에 서비스의 실행 파일 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-132">Include the name of the service's executable in the path provided to `binPath`.</span></span>

1. <span data-ttu-id="afb25-133">`sc start <SERVICE_NAME>` 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-133">Start the service with the `sc start <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="afb25-134">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-134">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="afb25-135">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-135">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="afb25-136">`sc query <SERVICE_NAME>` 명령을 사용하여 해당 상태를 확인하기 위해 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-136">The `sc query <SERVICE_NAME>` command can be used to check the status of the service to determine its status:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="afb25-137">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-137">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="afb25-138">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="afb25-138">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="afb25-139">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-139">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="afb25-140">`sc stop <SERVICE_NAME>` 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-140">Stop the service with the `sc stop <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="afb25-141">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-141">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="afb25-142">서비스를 중지하는 짧은 지연 후에 `sc delete <SERVICE_NAME>` 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-142">After a short delay to stop a service, uninstall the service with the `sc delete <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="afb25-143">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-143">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="afb25-144">이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-144">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="afb25-145">서비스 외부에서 실행할 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-145">Provide a way to run outside of a service</span></span>

<span data-ttu-id="afb25-146">서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-146">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="afb25-147">예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-147">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

<span data-ttu-id="afb25-148">ASP.NET Core 구성에 명령줄 인수에 대한 이름 값 쌍이 필요하기 때문에 인수가 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)에 전달되기 전에 `--console` 스위치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-148">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

> [!NOTE]
> <span data-ttu-id="afb25-149">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-149">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

::: moniker-end

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="afb25-150">이벤트 중지 및 시작 처리</span><span class="sxs-lookup"><span data-stu-id="afb25-150">Handle stopping and starting events</span></span>

<span data-ttu-id="afb25-151">[OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 및 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-151">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="afb25-152">[WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice)에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-152">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="afb25-153">사용자 지정 `WebHostService`를 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run)에 전달하는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-153">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="afb25-154">`Program.Main`에서 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) 대신 새 확장 메서드(`RunAsCustomService`)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-154">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   ::: moniker range=">= aspnetcore-2.0"

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=14)]

   > [!NOTE]
   > <span data-ttu-id="afb25-155">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-155">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

   ::: moniker-end

   ::: moniker range="< aspnetcore-2.0"

   [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=27)]

   ::: moniker-end

<span data-ttu-id="afb25-156">사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 속성에서 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-156">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="afb25-157">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="afb25-157">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="afb25-158">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="afb25-158">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="afb25-159">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afb25-159">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="kestrel-endpoint-configuration"></a><span data-ttu-id="afb25-160">Kestrel 엔드포인트 구성</span><span class="sxs-lookup"><span data-stu-id="afb25-160">Kestrel endpoint configuration</span></span>

<span data-ttu-id="afb25-161">HTTPS 구성 및 SNI 지원을 비롯한 Kestrel 엔드포인트 구성에 대한 자세한 내용은 [Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afb25-161">For information on Kestrel endpoint configuration, including HTTPS configuration and SNI support, see [Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>
