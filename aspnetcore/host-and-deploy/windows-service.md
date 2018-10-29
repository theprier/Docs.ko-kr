---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/25/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 7f19db0a1d12b904daff989bc969daf8d2302bfa
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325785"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="f404c-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="f404c-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="f404c-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f404c-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f404c-105">IIS를 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 사용하지 않고 Windows에서 ASP.NET Core 앱을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="f404c-106">Windows Service로 호스팅되는 앱은 재부팅 후 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="f404c-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="f404c-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="f404c-108">프로젝트를 Windows 서비스로 변환</span><span class="sxs-lookup"><span data-stu-id="f404c-108">Convert a project into a Windows Service</span></span>

<span data-ttu-id="f404c-109">기존 ASP.NET Core 프로젝트를 서비스로 실행되도록 설정하려면 다음과 같은 최소 변경 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-109">The following minimum changes are required to set up an existing ASP.NET Core project to run as a service:</span></span>

1. <span data-ttu-id="f404c-110">프로젝트 파일에서:</span><span class="sxs-lookup"><span data-stu-id="f404c-110">In the project file:</span></span>

   * <span data-ttu-id="f404c-111">Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)가 있는지 확인하거나, 대상 프레임워크가 포함된 `<PropertyGroup>`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-111">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add it to the `<PropertyGroup>` that contains the target framework:</span></span>

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

      <span data-ttu-id="f404c-112">여러 개의 RID를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="f404c-112">To publish for multiple RIDs:</span></span>

      * <span data-ttu-id="f404c-113">세미콜론으로 구분된 목록으로 RID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-113">Provide the RIDs in a semicolon-delimited list.</span></span>
      * <span data-ttu-id="f404c-114">속성 이름 `<RuntimeIdentifiers>`(복수)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-114">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

      <span data-ttu-id="f404c-115">자세한 내용은 [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f404c-115">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

   * <span data-ttu-id="f404c-116">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-116">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

1. <span data-ttu-id="f404c-117">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-117">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="f404c-118">`host.Run` 대신 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-118">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="f404c-119">[UseContentRoot](xref:fundamentals/host/web-host#content-root)를 호출하여 `Directory.GetCurrentDirectory()` 대신 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-119">Call [UseContentRoot](xref:fundamentals/host/web-host#content-root) and use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     ::: moniker range=">= aspnetcore-2.0"

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,16)]

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]

     ::: moniker-end

1. <span data-ttu-id="f404c-120">앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-120">Publish the app.</span></span> <span data-ttu-id="f404c-121">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 또는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-121">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles).</span></span> <span data-ttu-id="f404c-122">Visual Studio를 사용할 때 **FolderProfile**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-122">When using a Visual Studio, select the **FolderProfile**.</span></span>

   <span data-ttu-id="f404c-123">CLI(명령줄 인터페이스) 도구를 사용하여 샘플 앱을 게시하려면 프로젝트 폴더의 명령 프롬프트에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-123">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder.</span></span> <span data-ttu-id="f404c-124">프로젝트 파일의 `<RuntimeIdenfifier>`(또는 `<RuntimeIdentifiers>`) 속성에 RID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-124">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="f404c-125">다음 예제에서는 `win7-x64` 런타임에 대한 릴리스 구성에 앱이 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-125">In the following example, the app is published in Release configuration for the `win7-x64` runtime:</span></span>

   ```console
   dotnet publish --configuration Release --runtime win7-x64
   ```

1. <span data-ttu-id="f404c-126">[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-126">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="f404c-127">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-127">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="f404c-128">**경로의 시작 부분에서 등호와 인용 문자 사이에 공간이 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="f404c-128">**The space between the equal sign and the quote character at the start of the path is required.**</span></span>

   ```console
   sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"
   ```

   <span data-ttu-id="f404c-129">프로젝트 폴더에서 게시된 서비스의 경우 *publish* 폴더에 대한 경로를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-129">For a service published in the project folder, use the path to the *publish* folder to create the service.</span></span> <span data-ttu-id="f404c-130">다음 예제에서는</span><span class="sxs-lookup"><span data-stu-id="f404c-130">In the following example:</span></span>

   * <span data-ttu-id="f404c-131">프로젝트가 *c:\\my_services\\AspNetCoreService* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-131">The project resides in the *c:\\my_services\\AspNetCoreService* folder.</span></span>
   * <span data-ttu-id="f404c-132">프로젝트는 `Release` 구성에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-132">The project is published in `Release` configuration.</span></span>
   * <span data-ttu-id="f404c-133">TFM(대상 프레임워크 모니커)은 `netcoreapp2.1`입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-133">The Target Framework Moniker (TFM) is `netcoreapp2.1`.</span></span>
   * <span data-ttu-id="f404c-134">RID(런타임 ID)는 `win7-x64`입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-134">The Runtime Identifer (RID) is `win7-x64`.</span></span>
   * <span data-ttu-id="f404c-135">앱 실행 파일의 이름은 *AspNetCoreService.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-135">The app executable is named *AspNetCoreService.exe*.</span></span>
   * <span data-ttu-id="f404c-136">서비스의 이름은 **MyService**입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-136">The service is named **MyService**.</span></span>

   <span data-ttu-id="f404c-137">예제:</span><span class="sxs-lookup"><span data-stu-id="f404c-137">Example:</span></span>

   ```console
   sc create MyService binPath= "c:\my_services\AspNetCoreService\bin\Release\netcoreapp2.1\win7-x64\publish\AspNetCoreService.exe"
   ```

   > [!IMPORTANT]
   > <span data-ttu-id="f404c-138">`binPath=` 인수와 해당 값 사이에 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-138">Make sure the space is present between the `binPath=` argument and its value.</span></span>

   <span data-ttu-id="f404c-139">다른 폴더의 서비스를 게시하고 시작하려면:</span><span class="sxs-lookup"><span data-stu-id="f404c-139">To publish and start the service from a different folder:</span></span>

      * <span data-ttu-id="f404c-140">`dotnet publish` 명령에 대해 [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-140">Use the [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) option on the `dotnet publish` command.</span></span> <span data-ttu-id="f404c-141">Visual Studio를 사용하는 경우 **게시** 단추를 선택하기 전에 **FolderProfile** 게시 속성 페이지에 **대상 위치**를 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="f404c-141">If using Visual Studio, configure the **Target Location** in the **FolderProfile** publish property page before selecting the **Publish** button.</span></span>
      * <span data-ttu-id="f404c-142">출력 폴더 경로를 사용하는 `sc.exe` 명령으로 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-142">Create the service with the `sc.exe` command using the output folder path.</span></span> <span data-ttu-id="f404c-143">`binPath`에 제공된 경로에 서비스의 실행 파일 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-143">Include the name of the service's executable in the path provided to `binPath`.</span></span>

1. <span data-ttu-id="f404c-144">`sc start <SERVICE_NAME>` 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-144">Start the service with the `sc start <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="f404c-145">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-145">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="f404c-146">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-146">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="f404c-147">서비스 상태를 확인하려면 `sc query <SERVICE_NAME>` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-147">To check the status of the service, use the `sc query <SERVICE_NAME>` command.</span></span> <span data-ttu-id="f404c-148">상태는 다음 값 중 하나로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-148">The status is reported as one of the following values:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="f404c-149">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-149">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="f404c-150">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="f404c-150">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="f404c-151">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-151">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="f404c-152">`sc stop <SERVICE_NAME>` 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-152">Stop the service with the `sc stop <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="f404c-153">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-153">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="f404c-154">서비스를 중지하는 짧은 지연 후에 `sc delete <SERVICE_NAME>` 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-154">After a short delay to stop a service, uninstall the service with the `sc delete <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="f404c-155">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-155">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="f404c-156">이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-156">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="run-the-app-outside-of-a-service"></a><span data-ttu-id="f404c-157">서비스 외부에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="f404c-157">Run the app outside of a service</span></span>

<span data-ttu-id="f404c-158">서비스 외부에서 실행하면 테스트하고 디버그하기가 더 쉬우므로 특정 조건에서만 `RunAsService`를 호출하는 코드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-158">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="f404c-159">예를 들어 `--console` 명령줄 인수를 사용하거나 디버거가 연결된 경우 앱을 콘솔 앱으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-159">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

<span data-ttu-id="f404c-160">ASP.NET Core 구성에 명령줄 인수에 대한 이름 값 쌍이 필요하기 때문에 인수가 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)에 전달되기 전에 `--console` 스위치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-160">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

> [!NOTE]
> <span data-ttu-id="f404c-161">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-161">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

::: moniker-end

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="f404c-162">이벤트 중지 및 시작 처리</span><span class="sxs-lookup"><span data-stu-id="f404c-162">Handle stopping and starting events</span></span>

<span data-ttu-id="f404c-163">[OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 및 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 이벤트를 처리하려면 다음과 같이 추가로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-163">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="f404c-164">[WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice)에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-164">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="f404c-165">사용자 지정 `WebHostService`를 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run)에 전달하는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-165">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="f404c-166">`Program.Main`에서 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) 대신 새 확장 메서드(`RunAsCustomService`)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-166">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   ::: moniker range=">= aspnetcore-2.0"

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=17)]

   > [!NOTE]
   > <span data-ttu-id="f404c-167">[통합 테스트](xref:test/integration-tests)가 제대로 작동하려면 `CreateWebHostBuilder`의 서명이 `CreateWebHostBuilder(string[])`이어야 하므로 `isService`는 `Main`에서 `CreateWebHostBuilder`로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-167">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

   ::: moniker-end

   ::: moniker range="< aspnetcore-2.0"

   [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=27)]

   ::: moniker-end

<span data-ttu-id="f404c-168">사용자 지정 `WebHostService` 코드에 종속성 주입의 서비스(예: 로거)가 필요한 경우 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 속성에서 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-168">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="f404c-169">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="f404c-169">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="f404c-170">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-170">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="f404c-171">자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f404c-171">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="f404c-172">HTTPS 구성</span><span class="sxs-lookup"><span data-stu-id="f404c-172">Configure HTTPS</span></span>

<span data-ttu-id="f404c-173">[Kestrel 서버 HTTPS 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-173">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="f404c-174">현재 디렉터리 및 콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="f404c-174">Current directory and content root</span></span>

<span data-ttu-id="f404c-175">Windows 서비스에 대해 `Directory.GetCurrentDirectory()`를 호출하여 반환된 현재 작업 디렉터리는 *C:\\WINDOWS\\system32* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-175">The current working directory returned by calling `Directory.GetCurrentDirectory()` for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="f404c-176">*system32* 폴더는 서비스의 파일(예: 설정 파일)을 저장을 저장하는 데 적절한 위치가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-176">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="f404c-177">다음 방법 중 하나를 사용하여 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용할 때 [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath)로 서비스의 자산 및 설정 파일을 유지 관리 및 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-177">Use one of the following approaches to maintain and access a service's assets and settings files with [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) when using an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder):</span></span>

* <span data-ttu-id="f404c-178">콘텐츠 루트 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-178">Use the content root path.</span></span> <span data-ttu-id="f404c-179">`IHostingEnvironment.ContentRootPath`는 서비스가 만들어질 때 `binPath` 인수에 제공된 동일한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-179">The `IHostingEnvironment.ContentRootPath` is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="f404c-180">설정 파일에 대한 경로를 만들려면 `Directory.GetCurrentDirectory()`를 사용하는 대신 콘텐츠 루트 경로를 사용하고 앱의 콘텐츠 루트의 파일을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-180">Instead of using `Directory.GetCurrentDirectory()` to create paths to settings files, use the content root path and maintain the files in the app's content root.</span></span>
* <span data-ttu-id="f404c-181">디스크의 적합한 위치에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-181">Store the files in a suitable location on disk.</span></span> <span data-ttu-id="f404c-182">파일을 포함하는 폴더에 `SetBasePath`로 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f404c-182">Specify an absolute path with `SetBasePath` to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f404c-183">추가 자료</span><span class="sxs-lookup"><span data-stu-id="f404c-183">Additional resources</span></span>

* <span data-ttu-id="f404c-184">[Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)(HTTPS 구성 및 SNI 지원 포함)</span><span class="sxs-lookup"><span data-stu-id="f404c-184">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
