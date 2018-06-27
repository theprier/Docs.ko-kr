---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 0149039f69539b7c69d7ba45efcf09d80ffcba79
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275100"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="bcb36-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="bcb36-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="bcb36-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bcb36-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="bcb36-105">IIS를 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="bcb36-106">Windows 서비스로 호스트된 앱은 사용자 개입 없이 앱이 다시 부팅되거나 크래시된 후에 자동으로 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="bcb36-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="bcb36-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="get-started"></a><span data-ttu-id="bcb36-108">시작</span><span class="sxs-lookup"><span data-stu-id="bcb36-108">Get started</span></span>

<span data-ttu-id="bcb36-109">기존 ASP.NET Core 프로젝트를 서비스에서 실행하도록 설정하려면 다음과 같은 최소 변경 내용이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-109">The following minimum changes are required to set up an existing ASP.NET Core project to run in a service:</span></span>

1. <span data-ttu-id="bcb36-110">프로젝트 파일에서:</span><span class="sxs-lookup"><span data-stu-id="bcb36-110">In the project file:</span></span>

   1. <span data-ttu-id="bcb36-111">런타임 식별자의 존재 여부를 확인하거나 이를 대상 프레임워크를 포함하는 **\<PropertyGroup>** 에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-111">Confirm the presence of the runtime identifier or add it to the **\<PropertyGroup>** that contains the target framework:</span></span>
      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```
   1. <span data-ttu-id="bcb36-112">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-112">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

1. <span data-ttu-id="bcb36-113">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-113">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="bcb36-114">`host.Run` 대신 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-114">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="bcb36-115">코드가 `UseContentRoot`를 호출하는 경우 `Directory.GetCurrentDirectory()` 대신 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-115">If the code calls `UseContentRoot`, use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     ::: moniker range=">= aspnetcore-2.0"

     <span data-ttu-id="bcb36-116">[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,11)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-116">[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,11)]</span></span>

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     <span data-ttu-id="bcb36-117">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-117">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]</span></span>

     ::: moniker-end

1. <span data-ttu-id="bcb36-118">앱을 폴더에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-118">Publish the app to a folder.</span></span> <span data-ttu-id="bcb36-119">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 또는 폴더에 게시되는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-119">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

   <span data-ttu-id="bcb36-120">명령줄에서 샘플 앱을 게시하려면 프로젝트 폴더의 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-120">To publish the sample app from the command line, run the following command in a console window from the project folder:</span></span>

   ```console
   dotnet publish --configuration Release --output c:\svc
   ```

1. <span data-ttu-id="bcb36-121">[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만듭니다(`sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"`).</span><span class="sxs-lookup"><span data-stu-id="bcb36-121">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service (`sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"`).</span></span> <span data-ttu-id="bcb36-122">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-122">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="bcb36-123">**등호와 경로를 시작하는 인용 문자 사이에 공간이 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="bcb36-123">**The space between the equal sign and the quote character that starts the path is required.**</span></span>

   <span data-ttu-id="bcb36-124">샘플 앱 및 따라오는 명령의 경우 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-124">For the sample app and command that follows, the service is:</span></span>

   * <span data-ttu-id="bcb36-125">**MyService**라는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-125">Named **MyService**.</span></span>
   * <span data-ttu-id="bcb36-126">*c:\\svc* 폴더에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-126">Published to *c:\\svc* folder.</span></span>
   * <span data-ttu-id="bcb36-127">*AspNetCoreService.exe*라는 앱 실행 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-127">Has an app executable named *AspNetCoreService.exe*.</span></span>

   <span data-ttu-id="bcb36-128">관리자 권한으로 명령 셸을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-128">Open a command shell with administrative privileges and run the following command:</span></span>

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe"
   ```

   <span data-ttu-id="bcb36-129">**`binPath=` 인수 및 해당 값 사이에 공간이 있어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bcb36-129">**Make sure the space is present between the `binPath=` argument and its value.**</span></span>

1. <span data-ttu-id="bcb36-130">`sc start <SERVICE_NAME>` 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-130">Start the service with the `sc start <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="bcb36-131">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-131">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="bcb36-132">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-132">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="bcb36-133">`sc query <SERVICE_NAME>` 명령을 사용하여 해당 상태를 확인하기 위해 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-133">The `sc query <SERVICE_NAME>` command can be used to check the status of the service to determine its status:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="bcb36-134">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-134">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="bcb36-135">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="bcb36-135">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="bcb36-136">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-136">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="bcb36-137">`sc stop <SERVICE_NAME>` 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-137">Stop the service with the `sc stop <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="bcb36-138">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-138">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="bcb36-139">서비스를 중지하는 짧은 지연 후에 `sc delete <SERVICE_NAME>` 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-139">After a short delay to stop a service, uninstall the service with the `sc delete <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="bcb36-140">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-140">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="bcb36-141">이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-141">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="bcb36-142">서비스 외부에서 실행할 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-142">Provide a way to run outside of a service</span></span>

<span data-ttu-id="bcb36-143">서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-143">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="bcb36-144">예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-144">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="bcb36-145">[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-145">[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]</span></span>

<span data-ttu-id="bcb36-146">ASP.NET Core 구성에 명령줄 인수에 대한 이름 값 쌍이 필요하기 때문에 인수가 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)에 전달되기 전에 `--console` 스위치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-146">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="bcb36-147">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-147">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]</span></span>

::: moniker-end

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="bcb36-148">이벤트 중지 및 시작 처리</span><span class="sxs-lookup"><span data-stu-id="bcb36-148">Handle stopping and starting events</span></span>

<span data-ttu-id="bcb36-149">[OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 및 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-149">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="bcb36-150">[WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice)에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-150">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="bcb36-151">사용자 지정 `WebHostService`를 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run)에 전달하는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-151">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="bcb36-152">`Program.Main`에서 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) 대신 새 확장 메서드(`RunAsCustomService`)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-152">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   ::: moniker range=">= aspnetcore-2.0"

   <span data-ttu-id="bcb36-153">[!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=27)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-153">[!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=27)]</span></span>

   ::: moniker-end

   ::: moniker range="< aspnetcore-2.0"

   <span data-ttu-id="bcb36-154">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=27)]</span><span class="sxs-lookup"><span data-stu-id="bcb36-154">[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=27)]</span></span>

   ::: moniker-end

<span data-ttu-id="bcb36-155">사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 속성에서 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-155">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="bcb36-156">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="bcb36-156">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="bcb36-157">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb36-157">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="bcb36-158">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcb36-158">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="kestrel-endpoint-configuration"></a><span data-ttu-id="bcb36-159">Kestrel 엔드포인트 구성</span><span class="sxs-lookup"><span data-stu-id="bcb36-159">Kestrel endpoint configuration</span></span>

<span data-ttu-id="bcb36-160">HTTPS 구성 및 SNI 지원을 비롯한 Kestrel 엔드포인트 구성에 대한 자세한 내용은 [Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcb36-160">For information on Kestrel endpoint configuration, including HTTPS configuration and SNI support, see [Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>
