---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/22/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: eedaf64710506f2a2aac65c178a9888d2ab33d38
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837483"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="bb37e-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="bb37e-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="bb37e-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bb37e-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="bb37e-105">IIS를 사용하지 않고 Windows에서 ASP.NET Core 앱을 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-105">An ASP.NET Core app can be hosted on Windows as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications) without using IIS.</span></span> <span data-ttu-id="bb37e-106">Windows Service로 호스팅되는 앱은 재부팅 후 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="bb37e-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="bb37e-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="deployment-type"></a><span data-ttu-id="bb37e-108">배포 유형</span><span class="sxs-lookup"><span data-stu-id="bb37e-108">Deployment type</span></span>

<span data-ttu-id="bb37e-109">프레임워크 종속 또는 자체 포함 Windows 서비스 배포를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-109">You can create either a framework-dependent or self-contained Windows Service deployment.</span></span> <span data-ttu-id="bb37e-110">배포 시나리오에 대한 자세한 내용은 [.NET Core 애플리케이션 배포](/dotnet/core/deploying/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-110">For information and advice on deployment scenarios, see [.NET Core application deployment](/dotnet/core/deploying/).</span></span>

### <a name="framework-dependent-deployment"></a><span data-ttu-id="bb37e-111">프레임워크 종속 배포</span><span class="sxs-lookup"><span data-stu-id="bb37e-111">Framework-dependent deployment</span></span>

<span data-ttu-id="bb37e-112">FDD(프레임워크 종속 배포)에서는 대상 시스템에 .NET Core의 공유 시스템 차원 버전이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-112">Framework-dependent deployment (FDD) relies on the presence of a shared system-wide version of .NET Core on the target system.</span></span> <span data-ttu-id="bb37e-113">ASP.NET Core Windows 서비스 앱과 함께 FDD 시나리오를 사용하는 경우 SDK에서 *프레임워크 종속 실행 파일*이라는 실행 파일(*\*.exe*)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-113">When the FDD scenario is used with an ASP.NET Core Windows Service app, the SDK produces an executable (*\*.exe*), called a *framework-dependent executable*.</span></span>

### <a name="self-contained-deployment"></a><span data-ttu-id="bb37e-114">자체 포함 배포</span><span class="sxs-lookup"><span data-stu-id="bb37e-114">Self-contained deployment</span></span>

<span data-ttu-id="bb37e-115">SCD(자체 포함 배포)에서는 대상 시스템에 공유 구성 요소가 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-115">Self-contained deployment (SCD) doesn't rely on the presence of shared components on the target system.</span></span> <span data-ttu-id="bb37e-116">런타임 및 앱의 종속성이 앱과 함께 호스팅 시스템에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-116">The runtime and the app's dependencies are deployed with the app to the hosting system.</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="bb37e-117">프로젝트를 Windows 서비스로 변환</span><span class="sxs-lookup"><span data-stu-id="bb37e-117">Convert a project into a Windows Service</span></span>

<span data-ttu-id="bb37e-118">기존 ASP.NET Core 프로젝트를 다음과 같이 변경하여 앱을 서비스로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-118">Make the following changes to an existing ASP.NET Core project to run the app as a service:</span></span>

### <a name="project-file-updates"></a><span data-ttu-id="bb37e-119">프로젝트 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="bb37e-119">Project file updates</span></span>

<span data-ttu-id="bb37e-120">선택한 [배포 유형](#deployment-type)에 따라 프로젝트 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-120">Based on your choice of [deployment type](#deployment-type), update the project file:</span></span>

#### <a name="framework-dependent-deployment-fdd"></a><span data-ttu-id="bb37e-121">FDD(프레임워크 종속 배포)</span><span class="sxs-lookup"><span data-stu-id="bb37e-121">Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="bb37e-122">대상 프레임워크가 포함된 `<PropertyGroup>`에 Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-122">Add a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="bb37e-123">다음 예제에서는 RID가 `win7-x64`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-123">In the following example, the RID is set to `win7-x64`.</span></span> <span data-ttu-id="bb37e-124">`<SelfContained>` 속성을 `false`로 설정하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-124">Add the `<SelfContained>` property set to `false`.</span></span> <span data-ttu-id="bb37e-125">이러한 속성은 SDK가 Windows용 실행 파일(*.exe*)을 생성하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-125">These properties instruct the SDK to generate an executable (*.exe*) file for Windows.</span></span>

<span data-ttu-id="bb37e-126">ASP.NET Core 앱을 게시할 때 일반적으로 생성되는 *web.config* 파일은 Windows 서비스 앱에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-126">A *web.config* file, which is normally produced when publishing an ASP.NET Core app, is unnecessary for a Windows Services app.</span></span> <span data-ttu-id="bb37e-127">*web.config* 파일이 생성되지 않도록 하려면 `<IsTransformWebConfigDisabled>` 속성을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-127">To disable the creation of the *web.config* file, add the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="bb37e-128">`<UseAppHost>` 속성을 `true`로 설정하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-128">Add the `<UseAppHost>` property set to `true`.</span></span> <span data-ttu-id="bb37e-129">이 속성은 서비스에 FDD의 활성화 경로(실행 파일, *.exe*)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-129">This property provides the service with an activation path (an executable, *.exe*) for an FDD.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.1</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <UseAppHost>true</UseAppHost>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

#### <a name="self-contained-deployment-scd"></a><span data-ttu-id="bb37e-130">SCD(자체 포함 배포)</span><span class="sxs-lookup"><span data-stu-id="bb37e-130">Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="bb37e-131">Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)가 있는지 확인하거나, 대상 프레임워크가 포함된 `<PropertyGroup>`에 RID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-131">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add a RID to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="bb37e-132">`<IsTransformWebConfigDisabled>` 속성을 `true`로 설정하여 추가하면 *web.config* 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-132">Disable the creation of a *web.config* file by adding the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="bb37e-133">여러 개의 RID를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="bb37e-133">To publish for multiple RIDs:</span></span>

* <span data-ttu-id="bb37e-134">세미콜론으로 구분된 목록으로 RID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-134">Provide the RIDs in a semicolon-delimited list.</span></span>
* <span data-ttu-id="bb37e-135">속성 이름 `<RuntimeIdentifiers>`(복수)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-135">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

  <span data-ttu-id="bb37e-136">자세한 내용은 [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-136">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

<span data-ttu-id="bb37e-137">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-137">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

<span data-ttu-id="bb37e-138">Windows 이벤트 로그 로깅을 사용하도록 설정하려면 [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog)에 대한 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-138">To enable Windows Event Log logging, add a package reference for [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog).</span></span>

<span data-ttu-id="bb37e-139">자세한 내용은 [시작 및 중지 이벤트 처리](#handle-starting-and-stopping-events) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-139">For more information, see the [Handle starting and stopping events](#handle-starting-and-stopping-events) section.</span></span>

### <a name="programmain-updates"></a><span data-ttu-id="bb37e-140">Program.Main 업데이트</span><span class="sxs-lookup"><span data-stu-id="bb37e-140">Program.Main updates</span></span>

<span data-ttu-id="bb37e-141">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-141">Make the following changes in `Program.Main`:</span></span>

* <span data-ttu-id="bb37e-142">서비스 외부에서 실행할 때 테스트 및 디버그하려면 앱이 서비스 또는 콘솔 앱으로 실행되고 있는지 확인하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-142">To test and debug when running outside of a service, add code to determine if the app is running as a service or a console app.</span></span> <span data-ttu-id="bb37e-143">디버거가 연결되었는지 또는 `--console` 명령줄 인수가 있는지 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-143">Inspect if the debugger is attached or a `--console` command-line argument is present.</span></span>

  <span data-ttu-id="bb37e-144">두 조건 중 하나라도 true이면(앱이 서비스로 실행되지 않음) 웹 호스트에 대해 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-144">If either condition is true (the app isn't run as a service), call <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> on the Web Host.</span></span>

  <span data-ttu-id="bb37e-145">두 조건이 모두 false이면(앱이 서비스로 실행됨) 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-145">If the conditions are false (the app is run as a service):</span></span>

  * <span data-ttu-id="bb37e-146"><xref:System.IO.Directory.SetCurrentDirectory*>를 호출하고 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-146">Call <xref:System.IO.Directory.SetCurrentDirectory*> and use a path to the app's published location.</span></span> <span data-ttu-id="bb37e-147">`GetCurrentDirectory`를 호출하는 경우 Windows 서비스 앱이 *C:\\WINDOWS\\system32* 폴더를 반환하므로 경로를 얻기 위해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-147">Don't call <xref:System.IO.Directory.GetCurrentDirectory*> to obtain the path because a Windows Service app returns the *C:\\WINDOWS\\system32* folder when `GetCurrentDirectory` is called.</span></span> <span data-ttu-id="bb37e-148">자세한 내용은 [현재 디렉터리 및 콘텐츠 루트](#current-directory-and-content-root) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-148">For more information, see the [Current directory and content root](#current-directory-and-content-root) section.</span></span>
  * <span data-ttu-id="bb37e-149"><xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>를 호출하여 앱을 서비스로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-149">Call <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> to run the app as a service.</span></span>

  <span data-ttu-id="bb37e-150">[명령줄 구성 공급자](xref:fundamentals/configuration/index#command-line-configuration-provider)에는 명령줄 인수에 대한 이름-값 쌍이 필요하므로 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>가 수신하기 전에 `--console` 스위치가 인수에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-150">Because the [Command-line Configuration Provider](xref:fundamentals/configuration/index#command-line-configuration-provider) requires name-value pairs for command-line arguments, the `--console` switch is removed from the arguments before <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> receives them.</span></span>

* <span data-ttu-id="bb37e-151">Windows 이벤트 로그에 기록하려면 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>에 EventLog 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-151">To write to the Windows Event Log, add the EventLog provider to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>.</span></span> <span data-ttu-id="bb37e-152">*appsettings.Production.json* 파일에서 `Logging:LogLevel:Default` 키를 사용하여 로깅 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-152">Set the logging level with the `Logging:LogLevel:Default` key in the *appsettings.Production.json* file.</span></span> <span data-ttu-id="bb37e-153">데모 및 테스트 목적으로, 샘플 앱의 프로덕션 설정 파일에서는 로깅 수준이 `Information`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-153">For demonstration and testing purposes, the sample app's Production settings file sets the logging level to `Information`.</span></span> <span data-ttu-id="bb37e-154">프로덕션에서 이 값은 일반적으로 `Error`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-154">In production, the value is typically set to `Error`.</span></span> <span data-ttu-id="bb37e-155">자세한 내용은 <xref:fundamentals/logging/index#windows-eventlog-provider>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-155">For more information, see <xref:fundamentals/logging/index#windows-eventlog-provider>.</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

### <a name="publish-the-app"></a><span data-ttu-id="bb37e-156">앱 게시</span><span class="sxs-lookup"><span data-stu-id="bb37e-156">Publish the app</span></span>

<span data-ttu-id="bb37e-157">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish), [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 또는 Visual Studio Code를 사용하여 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-157">Publish the app using [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles), or Visual Studio Code.</span></span> <span data-ttu-id="bb37e-158">Visual Studio를 사용하는 경우 **FolderProfile**을 선택하고 **대상 위치**를 구성한 후 **게시** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-158">When using Visual Studio, select the **FolderProfile** and configure the **Target Location** before selecting the **Publish** button.</span></span>

<span data-ttu-id="bb37e-159">CLI(명령줄 인터페이스) 도구를 사용하여 샘플 앱을 게시하려면 [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) 옵션에 릴리스 구성을 전달하여 프로젝트 폴더의 명령 프롬프트에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-159">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder with a Release configuration passed to the [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) option.</span></span> <span data-ttu-id="bb37e-160">앱 외부 폴더에 게시하려면 [-o|--output](/dotnet/core/tools/dotnet-publish#options) 옵션에 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-160">Use the [-o|--output](/dotnet/core/tools/dotnet-publish#options) option with a path to publish to a folder outside of the app.</span></span>

#### <a name="publish-a-framework-dependent-deployment-fdd"></a><span data-ttu-id="bb37e-161">FDD(프레임워크 종속 배포) 게시</span><span class="sxs-lookup"><span data-stu-id="bb37e-161">Publish a Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="bb37e-162">다음 예제에서는 앱이 *c:\\svc* 폴더에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-162">In the following example, the app is published to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --output c:\svc
```

#### <a name="publish-a-self-contained-deployment-scd"></a><span data-ttu-id="bb37e-163">SCD(자체 포함 배포) 게시</span><span class="sxs-lookup"><span data-stu-id="bb37e-163">Publish a Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="bb37e-164">프로젝트 파일의 `<RuntimeIdenfifier>`(또는 `<RuntimeIdentifiers>`) 속성에 RID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-164">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="bb37e-165">`dotnet publish` 명령의 [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) 옵션에 런타임을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-165">Supply the runtime to the [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) option of the `dotnet publish` command.</span></span>

<span data-ttu-id="bb37e-166">다음 예제에서는 앱이 `win7-x64` 런타임의 *c:\\svc* 폴더에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-166">In the following example, the app is published for the `win7-x64` runtime to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

### <a name="create-a-user-account"></a><span data-ttu-id="bb37e-167">사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="bb37e-167">Create a user account</span></span>

<span data-ttu-id="bb37e-168">`net user` 명령을 사용하여 서비스에 대한 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-168">Create a user account for the service using the `net user` command:</span></span>

```console
net user {USER ACCOUNT} {PASSWORD} /add
```

<span data-ttu-id="bb37e-169">샘플 앱의 경우, 이름이 `ServiceUser`인 사용자 계정과 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-169">For the sample app, create a user account with the name `ServiceUser` and a password.</span></span> <span data-ttu-id="bb37e-170">다음 명령에서 `{PASSWORD}`를 [강력한 암호](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-170">In the following command, replace `{PASSWORD}` with a [strong password](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span></span>

```console
net user ServiceUser {PASSWORD} /add
```

<span data-ttu-id="bb37e-171">그룹에 사용자를 추가해야 하는 경우 `net localgroup` 명령을 사용합니다. 여기서 `{GROUP}`은 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-171">If you need to add the user to a group, use the `net localgroup` command, where `{GROUP}` is the name of the group:</span></span>

```console
net localgroup {GROUP} {USER ACCOUNT} /add
```

<span data-ttu-id="bb37e-172">자세한 내용은 [서비스 사용자 계정](/windows/desktop/services/service-user-accounts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-172">For more information, see [Service User Accounts](/windows/desktop/services/service-user-accounts).</span></span>

### <a name="set-permissions"></a><span data-ttu-id="bb37e-173">권한 설정</span><span class="sxs-lookup"><span data-stu-id="bb37e-173">Set permissions</span></span>

<span data-ttu-id="bb37e-174">[icacls](/windows-server/administration/windows-commands/icacls) 명령을 사용하여 앱의 폴더에 쓰기/읽기/실행 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-174">Grant write/read/execute access to the app's folder using the [icacls](/windows-server/administration/windows-commands/icacls) command:</span></span>

```console
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* <span data-ttu-id="bb37e-175">`{PATH}` &ndash; 앱의 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-175">`{PATH}` &ndash; Path to the app's folder.</span></span>
* <span data-ttu-id="bb37e-176">`{USER ACCOUNT}` &ndash; 사용자 계정(SID)입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-176">`{USER ACCOUNT}` &ndash; The user account (SID).</span></span>
* <span data-ttu-id="bb37e-177">`(OI)` &ndash; 개체 상속 플래그는 권한을 하위 파일에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-177">`(OI)` &ndash; The Object Inherit flag propagates permissions to subordinate files.</span></span>
* <span data-ttu-id="bb37e-178">`(CI)` &ndash; 컨테이너 상속 플래그는 권한을 하위 폴더에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-178">`(CI)` &ndash; The Container Inherit flag propagates permissions to subordinate folders.</span></span>
* <span data-ttu-id="bb37e-179">`{PERMISSION FLAGS}` &ndash; 앱의 액세스 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-179">`{PERMISSION FLAGS}` &ndash; Sets the app's access permissions.</span></span>
  * <span data-ttu-id="bb37e-180">쓰기(`W`)</span><span class="sxs-lookup"><span data-stu-id="bb37e-180">Write (`W`)</span></span>
  * <span data-ttu-id="bb37e-181">읽기(`R`)</span><span class="sxs-lookup"><span data-stu-id="bb37e-181">Read (`R`)</span></span>
  * <span data-ttu-id="bb37e-182">실행(`X`)</span><span class="sxs-lookup"><span data-stu-id="bb37e-182">Execute (`X`)</span></span>
  * <span data-ttu-id="bb37e-183">전체(`F`)</span><span class="sxs-lookup"><span data-stu-id="bb37e-183">Full (`F`)</span></span>
  * <span data-ttu-id="bb37e-184">수정(`M`)</span><span class="sxs-lookup"><span data-stu-id="bb37e-184">Modify (`M`)</span></span>
* <span data-ttu-id="bb37e-185">`/t` &ndash; 기존 하위 폴더 및 파일에 재귀적으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-185">`/t` &ndash; Apply recursively to existing subordinate folders and files.</span></span>

<span data-ttu-id="bb37e-186">*c:\\svc* 폴더에 게시된 샘플 앱과 쓰기/읽기/실행 권한이 있는 `ServiceUser` 계정의 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-186">For the sample app published to the *c:\\svc* folder and the `ServiceUser` account with write/read/execute permissions, use the following command:</span></span>

```console
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

<span data-ttu-id="bb37e-187">자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-187">For more information, see [icacls](/windows-server/administration/windows-commands/icacls).</span></span>

## <a name="manage-the-service"></a><span data-ttu-id="bb37e-188">서비스 관리</span><span class="sxs-lookup"><span data-stu-id="bb37e-188">Manage the service</span></span>

### <a name="create-the-service"></a><span data-ttu-id="bb37e-189">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="bb37e-189">Create the service</span></span>

<span data-ttu-id="bb37e-190">[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-190">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="bb37e-191">`binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-191">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="bb37e-192">**각 매개 변수의 등호 및 인용 문자 값 사이에 공백이 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="bb37e-192">**The space between the equal sign and the quote character of each parameter and value is required.**</span></span>

```console
sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
```

* <span data-ttu-id="bb37e-193">`{SERVICE NAME}` &ndash; [서비스 제어 관리자](/windows/desktop/services/service-control-manager)의 서비스에 할당하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-193">`{SERVICE NAME}` &ndash; The name to assign to the service in [Service Control Manager](/windows/desktop/services/service-control-manager).</span></span>
* <span data-ttu-id="bb37e-194">`{PATH}` &ndash; 서비스 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-194">`{PATH}` &ndash; The path to the service executable.</span></span>
* <span data-ttu-id="bb37e-195">`{DOMAIN}` &ndash; 도메인 가입 머신의 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-195">`{DOMAIN}` &ndash; The domain of a domain-joined machine.</span></span> <span data-ttu-id="bb37e-196">도메인에 가입되지 않은 머신의 경우 로컬 머신 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-196">If the machine isn't domain-joined, the local machine name.</span></span>
* <span data-ttu-id="bb37e-197">`{USER ACCOUNT}` &ndash; 서비스 실행에 사용되는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-197">`{USER ACCOUNT}` &ndash; The user account under which the service runs.</span></span>
* <span data-ttu-id="bb37e-198">`{PASSWORD}` &ndash; 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-198">`{PASSWORD}` &ndash; The user account password.</span></span>

> [!WARNING]
> <span data-ttu-id="bb37e-199">`obj` 매개 변수를 생략하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="bb37e-199">Do **not** omit the `obj` parameter.</span></span> <span data-ttu-id="bb37e-200">`obj`의 기본값은 [LocalSystem 계정](/windows/desktop/services/localsystem-account) 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-200">The default value for `obj` is the [LocalSystem account](/windows/desktop/services/localsystem-account) account.</span></span> <span data-ttu-id="bb37e-201">`LocalSystem` 계정으로 서비스를 실행하면 상당한 보안 위험이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-201">Running a service under the `LocalSystem` account presents a significant security risk.</span></span> <span data-ttu-id="bb37e-202">항상 제한된 권한을 가진 사용자 계정으로 서비스를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-202">Always run a service with a user account that has restricted privileges.</span></span>

<span data-ttu-id="bb37e-203">샘플 앱에 대한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-203">In the following example for the sample app:</span></span>

* <span data-ttu-id="bb37e-204">서비스의 이름은 **MyService**입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-204">The service is named **MyService**.</span></span>
* <span data-ttu-id="bb37e-205">게시된 서비스는 *c:\\svc* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-205">The published service resides in the *c:\\svc* folder.</span></span> <span data-ttu-id="bb37e-206">앱 실행 파일의 이름은 *SampleApp.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-206">The app executable is named *SampleApp.exe*.</span></span> <span data-ttu-id="bb37e-207">`binPath` 값을 큰따옴표(")로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-207">Enclose the `binPath` value in double quotation marks (").</span></span>
* <span data-ttu-id="bb37e-208">서비스는 `ServiceUser` 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-208">The service runs under the `ServiceUser` account.</span></span> <span data-ttu-id="bb37e-209">`{DOMAIN}`을 사용자 계정의 도메인 또는 로컬 머신 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-209">Replace `{DOMAIN}` with the user account's domain or local machine name.</span></span> <span data-ttu-id="bb37e-210">`obj` 값을 큰따옴표(")로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-210">Enclose the `obj` value in double quotation marks (").</span></span> <span data-ttu-id="bb37e-211">예제: 호스팅 시스템이 `MairaPC`라는 로컬 머신인 경우 `obj`를 `"MairaPC\ServiceUser"`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-211">Example: If the hosting system is a local machine named `MairaPC`, set `obj` to `"MairaPC\ServiceUser"`.</span></span>
* <span data-ttu-id="bb37e-212">`{PASSWORD}`를 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-212">Replace `{PASSWORD}` with the user account's password.</span></span> <span data-ttu-id="bb37e-213">`password` 값을 큰따옴표(")로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-213">Enclose the `password` value in double quotation marks (").</span></span>

```console
sc create MyService binPath= "c:\svc\sampleapp.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
```

> [!IMPORTANT]
> <span data-ttu-id="bb37e-214">매개 변수의 등호와 매개 변수의 값 사이에 공백이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-214">Make sure that the spaces between the parameters' equal signs and the parameters' values are present.</span></span>

### <a name="start-the-service"></a><span data-ttu-id="bb37e-215">서비스 시작</span><span class="sxs-lookup"><span data-stu-id="bb37e-215">Start the service</span></span>

<span data-ttu-id="bb37e-216">`sc start {SERVICE NAME}` 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-216">Start the service with the `sc start {SERVICE NAME}` command.</span></span>

<span data-ttu-id="bb37e-217">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-217">To start the sample app service, use the following command:</span></span>

```console
sc start MyService
```

<span data-ttu-id="bb37e-218">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-218">The command takes a few seconds to start the service.</span></span>

### <a name="determine-the-service-status"></a><span data-ttu-id="bb37e-219">서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="bb37e-219">Determine the service status</span></span>

<span data-ttu-id="bb37e-220">서비스 상태를 확인하려면 `sc query {SERVICE NAME}` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-220">To check the status of the service, use the `sc query {SERVICE NAME}` command.</span></span> <span data-ttu-id="bb37e-221">상태는 다음 값 중 하나로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-221">The status is reported as one of the following values:</span></span>

* `START_PENDING`
* `RUNNING`
* `STOP_PENDING`
* `STOPPED`

<span data-ttu-id="bb37e-222">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-222">Use the following command to check the status of the sample app service:</span></span>

```console
sc query MyService
```

### <a name="browse-a-web-app-service"></a><span data-ttu-id="bb37e-223">웹앱 서비스 찾아보기</span><span class="sxs-lookup"><span data-stu-id="bb37e-223">Browse a web app service</span></span>

<span data-ttu-id="bb37e-224">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="bb37e-224">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

<span data-ttu-id="bb37e-225">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-225">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

### <a name="stop-the-service"></a><span data-ttu-id="bb37e-226">서비스를 중지하여</span><span class="sxs-lookup"><span data-stu-id="bb37e-226">Stop the service</span></span>

<span data-ttu-id="bb37e-227">`sc stop {SERVICE NAME}` 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-227">Stop the service with the `sc stop {SERVICE NAME}` command.</span></span>

<span data-ttu-id="bb37e-228">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-228">The following command stops the sample app service:</span></span>

```console
sc stop MyService
```

### <a name="delete-the-service"></a><span data-ttu-id="bb37e-229">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="bb37e-229">Delete the service</span></span>

<span data-ttu-id="bb37e-230">서비스를 중지하는 짧은 지연 후에 `sc delete {SERVICE NAME}` 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-230">After a short delay to stop a service, uninstall the service with the `sc delete {SERVICE NAME}` command.</span></span>

<span data-ttu-id="bb37e-231">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-231">Check the status of the sample app service:</span></span>

```console
sc query MyService
```

<span data-ttu-id="bb37e-232">이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-232">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

```console
sc delete MyService
```

## <a name="handle-starting-and-stopping-events"></a><span data-ttu-id="bb37e-233">시작 및 중지 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="bb37e-233">Handle starting and stopping events</span></span>

<span data-ttu-id="bb37e-234"><xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*> 및 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> 이벤트를 처리하려면 추가로 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-234">To handle <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*>, and <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> events, perform the following additional changes:</span></span>

1. <span data-ttu-id="bb37e-235">`OnStarting`, `OnStarted` 및 `OnStopping` 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService>에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-235">Create a class that derives from <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService> with the `OnStarting`, `OnStarted`, and `OnStopping` methods:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. <span data-ttu-id="bb37e-236">`CustomWebHostService`를 <xref:System.ServiceProcess.ServiceBase.Run*>에 전달하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost>에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-236">Create an extension method for <xref:Microsoft.AspNetCore.Hosting.IWebHost> that passes the `CustomWebHostService` to <xref:System.ServiceProcess.ServiceBase.Run*>:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="bb37e-237">`Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> 대신 `RunAsCustomService` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-237">In `Program.Main`, call the `RunAsCustomService` extension method instead of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>:</span></span>

   ```csharp
   host.RunAsCustomService();
   ```

   <span data-ttu-id="bb37e-238">`Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>의 위치를 확인하려면 [프로젝트를 Windows 서비스로 변환](#convert-a-project-into-a-windows-service) 섹션에 표시된 코드 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-238">To see the location of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> in `Program.Main`, refer to the code sample shown in the [Convert a project into a Windows Service](#convert-a-project-into-a-windows-service) section.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="bb37e-239">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="bb37e-239">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="bb37e-240">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-240">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="bb37e-241">자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb37e-241">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="bb37e-242">HTTPS 구성</span><span class="sxs-lookup"><span data-stu-id="bb37e-242">Configure HTTPS</span></span>

<span data-ttu-id="bb37e-243">보안 엔드포인트로 서비스를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-243">To configure the service with a secure endpoint:</span></span>

1. <span data-ttu-id="bb37e-244">플랫폼의 인증서 획득 및 배포 메커니즘을 사용하여 호스팅 시스템에 대한 X.509 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-244">Create an X.509 certificate for the hosting system using your platform's certificate acquisition and deployment mechanisms.</span></span>

1. <span data-ttu-id="bb37e-245">[Kestrel 서버 HTTPS 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 지정하여 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-245">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) to use the certificate.</span></span>

<span data-ttu-id="bb37e-246">서비스 엔드포인트를 보호하기 위해 ASP.NET Core HTTPS 개발 인증서 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-246">Use of the ASP.NET Core HTTPS development certificate to secure a service endpoint isn't supported.</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="bb37e-247">현재 디렉터리 및 콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="bb37e-247">Current directory and content root</span></span>

<span data-ttu-id="bb37e-248">Windows 서비스에 대해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하여 반환된 현재 작업 디렉터리는 *C:\\WINDOWS\\system32* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-248">The current working directory returned by calling <xref:System.IO.Directory.GetCurrentDirectory*> for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="bb37e-249">*system32* 폴더는 서비스의 파일(예: 설정 파일)을 저장을 저장하는 데 적절한 위치가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-249">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="bb37e-250">다음 방법 중 하나를 사용하여 서비스의 자산 및 설정 파일을 유지 관리하고 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-250">Use one of the following approaches to maintain and access a service's assets and settings files.</span></span>

### <a name="set-the-content-root-path-to-the-apps-folder"></a><span data-ttu-id="bb37e-251">콘텐츠 루트 경로를 앱 폴더로 설정</span><span class="sxs-lookup"><span data-stu-id="bb37e-251">Set the content root path to the app's folder</span></span>

<span data-ttu-id="bb37e-252"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*>는 서비스가 만들어질 때 `binPath` 인수에 제공된 동일한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-252">The <xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="bb37e-253">`GetCurrentDirectory`를 호출하여 설정 파일의 경로를 만드는 대신, 앱의 콘텐츠 루트 경로를 사용하여 <xref:System.IO.Directory.SetCurrentDirectory*>를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-253">Instead of calling `GetCurrentDirectory` to create paths to settings files, call <xref:System.IO.Directory.SetCurrentDirectory*> with the path to the app's content root.</span></span>

<span data-ttu-id="bb37e-254">`Program.Main`에서 서비스 실행 파일의 폴더 경로를 확인하고 이 경로를 사용하여 앱의 콘텐츠 루트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-254">In `Program.Main`, determine the path to the folder of the service's executable and use the path to establish the app's content root:</span></span>

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a><span data-ttu-id="bb37e-255">디스크의 적합한 위치에 서비스 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-255">Store the service's files in a suitable location on disk</span></span>

<span data-ttu-id="bb37e-256">파일이 포함된 폴더로 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>를 사용하는 경우 <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>를 통해 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb37e-256">Specify an absolute path with <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> when using an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb37e-257">추가 자료</span><span class="sxs-lookup"><span data-stu-id="bb37e-257">Additional resources</span></span>

* <span data-ttu-id="bb37e-258">[Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)(HTTPS 구성 및 SNI 지원 포함)</span><span class="sxs-lookup"><span data-stu-id="bb37e-258">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>
