---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/08/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: ecc7f3a8cd813c2803d03294e38d726905eeb1b8
ms.sourcegitcommit: 34bf9fc6ea814c039401fca174642f0acb14be3c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57841425"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="5b8f3-103">Windows 서비스에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="5b8f3-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="5b8f3-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="5b8f3-105">IIS를 사용하지 않고 Windows에서 ASP.NET Core 앱을 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-105">An ASP.NET Core app can be hosted on Windows as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications) without using IIS.</span></span> <span data-ttu-id="5b8f3-106">Windows Service로 호스팅되는 앱은 재부팅 후 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-106">When hosted as a Windows Service, the app automatically starts after reboots.</span></span>

<span data-ttu-id="5b8f3-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5b8f3-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b8f3-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="5b8f3-108">Prerequisites</span></span>

* [<span data-ttu-id="5b8f3-109">PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="5b8f3-109">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell)

## <a name="deployment-type"></a><span data-ttu-id="5b8f3-110">배포 유형</span><span class="sxs-lookup"><span data-stu-id="5b8f3-110">Deployment type</span></span>

<span data-ttu-id="5b8f3-111">프레임워크 종속 또는 자체 포함 Windows 서비스 배포를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-111">You can create either a framework-dependent or self-contained Windows Service deployment.</span></span> <span data-ttu-id="5b8f3-112">배포 시나리오에 대한 자세한 내용은 [.NET Core 애플리케이션 배포](/dotnet/core/deploying/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-112">For information and advice on deployment scenarios, see [.NET Core application deployment](/dotnet/core/deploying/).</span></span>

### <a name="framework-dependent-deployment"></a><span data-ttu-id="5b8f3-113">프레임워크 종속 배포</span><span class="sxs-lookup"><span data-stu-id="5b8f3-113">Framework-dependent deployment</span></span>

<span data-ttu-id="5b8f3-114">FDD(프레임워크 종속 배포)에서는 대상 시스템에 .NET Core의 공유 시스템 차원 버전이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-114">Framework-dependent deployment (FDD) relies on the presence of a shared system-wide version of .NET Core on the target system.</span></span> <span data-ttu-id="5b8f3-115">ASP.NET Core Windows 서비스 앱과 함께 FDD 시나리오를 사용하는 경우 SDK에서 *프레임워크 종속 실행 파일*이라는 실행 파일(*\*.exe*)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-115">When the FDD scenario is used with an ASP.NET Core Windows Service app, the SDK produces an executable (*\*.exe*), called a *framework-dependent executable*.</span></span>

### <a name="self-contained-deployment"></a><span data-ttu-id="5b8f3-116">자체 포함 배포</span><span class="sxs-lookup"><span data-stu-id="5b8f3-116">Self-contained deployment</span></span>

<span data-ttu-id="5b8f3-117">SCD(자체 포함 배포)에서는 대상 시스템에 공유 구성 요소가 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-117">Self-contained deployment (SCD) doesn't rely on the presence of shared components on the target system.</span></span> <span data-ttu-id="5b8f3-118">런타임 및 앱의 종속성이 앱과 함께 호스팅 시스템에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-118">The runtime and the app's dependencies are deployed with the app to the hosting system.</span></span>

## <a name="convert-a-project-into-a-windows-service"></a><span data-ttu-id="5b8f3-119">프로젝트를 Windows 서비스로 변환</span><span class="sxs-lookup"><span data-stu-id="5b8f3-119">Convert a project into a Windows Service</span></span>

<span data-ttu-id="5b8f3-120">기존 ASP.NET Core 프로젝트를 다음과 같이 변경하여 앱을 서비스로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-120">Make the following changes to an existing ASP.NET Core project to run the app as a service:</span></span>

### <a name="project-file-updates"></a><span data-ttu-id="5b8f3-121">프로젝트 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="5b8f3-121">Project file updates</span></span>

<span data-ttu-id="5b8f3-122">선택한 [배포 유형](#deployment-type)에 따라 프로젝트 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-122">Based on your choice of [deployment type](#deployment-type), update the project file:</span></span>

#### <a name="framework-dependent-deployment-fdd"></a><span data-ttu-id="5b8f3-123">FDD(프레임워크 종속 배포)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-123">Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="5b8f3-124">대상 프레임워크가 포함된 `<PropertyGroup>`에 Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-124">Add a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="5b8f3-125">다음 예제에서는 RID가 `win7-x64`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-125">In the following example, the RID is set to `win7-x64`.</span></span> <span data-ttu-id="5b8f3-126">`<SelfContained>` 속성을 `false`로 설정하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-126">Add the `<SelfContained>` property set to `false`.</span></span> <span data-ttu-id="5b8f3-127">이러한 속성은 SDK가 Windows용 실행 파일(*.exe*)을 생성하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-127">These properties instruct the SDK to generate an executable (*.exe*) file for Windows.</span></span>

<span data-ttu-id="5b8f3-128">ASP.NET Core 앱을 게시할 때 일반적으로 생성되는 *web.config* 파일은 Windows 서비스 앱에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-128">A *web.config* file, which is normally produced when publishing an ASP.NET Core app, is unnecessary for a Windows Services app.</span></span> <span data-ttu-id="5b8f3-129">*web.config* 파일이 생성되지 않도록 하려면 `<IsTransformWebConfigDisabled>` 속성을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-129">To disable the creation of the *web.config* file, add the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

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

<span data-ttu-id="5b8f3-130">`<UseAppHost>` 속성을 `true`로 설정하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-130">Add the `<UseAppHost>` property set to `true`.</span></span> <span data-ttu-id="5b8f3-131">이 속성은 서비스에 FDD의 활성화 경로(실행 파일, *.exe*)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-131">This property provides the service with an activation path (an executable, *.exe*) for an FDD.</span></span>

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

#### <a name="self-contained-deployment-scd"></a><span data-ttu-id="5b8f3-132">SCD(자체 포함 배포)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-132">Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="5b8f3-133">Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)가 있는지 확인하거나, 대상 프레임워크가 포함된 `<PropertyGroup>`에 RID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-133">Confirm the presence of a Windows [Runtime Identifier (RID)](/dotnet/core/rid-catalog) or add a RID to the `<PropertyGroup>` that contains the target framework.</span></span> <span data-ttu-id="5b8f3-134">`<IsTransformWebConfigDisabled>` 속성을 `true`로 설정하여 추가하면 *web.config* 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-134">Disable the creation of a *web.config* file by adding the `<IsTransformWebConfigDisabled>` property set to `true`.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="5b8f3-135">여러 개의 RID를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="5b8f3-135">To publish for multiple RIDs:</span></span>

* <span data-ttu-id="5b8f3-136">세미콜론으로 구분된 목록으로 RID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-136">Provide the RIDs in a semicolon-delimited list.</span></span>
* <span data-ttu-id="5b8f3-137">속성 이름 `<RuntimeIdentifiers>`(복수)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-137">Use the property name `<RuntimeIdentifiers>` (plural).</span></span>

  <span data-ttu-id="5b8f3-138">자세한 내용은 [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-138">For more information, see [.NET Core RID Catalog](/dotnet/core/rid-catalog).</span></span>

<span data-ttu-id="5b8f3-139">[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-139">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices).</span></span>

<span data-ttu-id="5b8f3-140">Windows 이벤트 로그 로깅을 사용하도록 설정하려면 [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog)에 대한 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-140">To enable Windows Event Log logging, add a package reference for [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog).</span></span>

<span data-ttu-id="5b8f3-141">자세한 내용은 [시작 및 중지 이벤트 처리](#handle-starting-and-stopping-events) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-141">For more information, see the [Handle starting and stopping events](#handle-starting-and-stopping-events) section.</span></span>

### <a name="programmain-updates"></a><span data-ttu-id="5b8f3-142">Program.Main 업데이트</span><span class="sxs-lookup"><span data-stu-id="5b8f3-142">Program.Main updates</span></span>

<span data-ttu-id="5b8f3-143">`Program.Main`에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-143">Make the following changes in `Program.Main`:</span></span>

* <span data-ttu-id="5b8f3-144">서비스 외부에서 실행할 때 테스트 및 디버그하려면 앱이 서비스 또는 콘솔 앱으로 실행되고 있는지 확인하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-144">To test and debug when running outside of a service, add code to determine if the app is running as a service or a console app.</span></span> <span data-ttu-id="5b8f3-145">디버거가 연결되었는지 또는 `--console` 명령줄 인수가 있는지 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-145">Inspect if the debugger is attached or a `--console` command-line argument is present.</span></span>

  <span data-ttu-id="5b8f3-146">두 조건 중 하나라도 true이면(앱이 서비스로 실행되지 않음) 웹 호스트에 대해 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-146">If either condition is true (the app isn't run as a service), call <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> on the Web Host.</span></span>

  <span data-ttu-id="5b8f3-147">두 조건이 모두 false이면(앱이 서비스로 실행됨) 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-147">If the conditions are false (the app is run as a service):</span></span>

  * <span data-ttu-id="5b8f3-148"><xref:System.IO.Directory.SetCurrentDirectory*>를 호출하고 앱의 게시 위치에 대한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-148">Call <xref:System.IO.Directory.SetCurrentDirectory*> and use a path to the app's published location.</span></span> <span data-ttu-id="5b8f3-149"><xref:System.IO.Directory.GetCurrentDirectory*>를 호출하는 경우 Windows 서비스 앱이 *C:\\WINDOWS\\system32* 폴더를 반환하므로 경로를 얻기 위해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-149">Don't call <xref:System.IO.Directory.GetCurrentDirectory*> to obtain the path because a Windows Service app returns the *C:\\WINDOWS\\system32* folder when <xref:System.IO.Directory.GetCurrentDirectory*> is called.</span></span> <span data-ttu-id="5b8f3-150">자세한 내용은 [현재 디렉터리 및 콘텐츠 루트](#current-directory-and-content-root) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-150">For more information, see the [Current directory and content root](#current-directory-and-content-root) section.</span></span>
  * <span data-ttu-id="5b8f3-151"><xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>를 호출하여 앱을 서비스로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-151">Call <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> to run the app as a service.</span></span>

  <span data-ttu-id="5b8f3-152">[명령줄 구성 공급자](xref:fundamentals/configuration/index#command-line-configuration-provider)에는 명령줄 인수에 대한 이름-값 쌍이 필요하므로 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>가 수신하기 전에 `--console` 스위치가 인수에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-152">Because the [Command-line Configuration Provider](xref:fundamentals/configuration/index#command-line-configuration-provider) requires name-value pairs for command-line arguments, the `--console` switch is removed from the arguments before <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> receives them.</span></span>

* <span data-ttu-id="5b8f3-153">Windows 이벤트 로그에 기록하려면 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>에 EventLog 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-153">To write to the Windows Event Log, add the EventLog provider to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>.</span></span> <span data-ttu-id="5b8f3-154">*appsettings.Production.json* 파일에서 `Logging:LogLevel:Default` 키를 사용하여 로깅 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-154">Set the logging level with the `Logging:LogLevel:Default` key in the *appsettings.Production.json* file.</span></span> <span data-ttu-id="5b8f3-155">데모 및 테스트 목적으로, 샘플 앱의 프로덕션 설정 파일에서는 로깅 수준이 `Information`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-155">For demonstration and testing purposes, the sample app's Production settings file sets the logging level to `Information`.</span></span> <span data-ttu-id="5b8f3-156">프로덕션에서 이 값은 일반적으로 `Error`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-156">In production, the value is typically set to `Error`.</span></span> <span data-ttu-id="5b8f3-157">자세한 내용은 <xref:fundamentals/logging/index#windows-eventlog-provider>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-157">For more information, see <xref:fundamentals/logging/index#windows-eventlog-provider>.</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

## <a name="publish-the-app"></a><span data-ttu-id="5b8f3-158">앱 게시</span><span class="sxs-lookup"><span data-stu-id="5b8f3-158">Publish the app</span></span>

<span data-ttu-id="5b8f3-159">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish), [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 또는 Visual Studio Code를 사용하여 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-159">Publish the app using [dotnet publish](/dotnet/articles/core/tools/dotnet-publish), a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles), or Visual Studio Code.</span></span> <span data-ttu-id="5b8f3-160">Visual Studio를 사용하는 경우 **FolderProfile**을 선택하고 **대상 위치**를 구성한 후 **게시** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-160">When using Visual Studio, select the **FolderProfile** and configure the **Target Location** before selecting the **Publish** button.</span></span>

<span data-ttu-id="5b8f3-161">CLI(명령줄 인터페이스) 도구를 사용하여 샘플 앱을 게시하려면 [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) 옵션에 릴리스 구성을 전달하여 프로젝트 폴더의 명령 프롬프트에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-161">To publish the sample app using command-line interface (CLI) tools, run the [dotnet publish](/dotnet/core/tools/dotnet-publish) command at a command prompt from the project folder with a Release configuration passed to the [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) option.</span></span> <span data-ttu-id="5b8f3-162">앱 외부 폴더에 게시하려면 [-o|--output](/dotnet/core/tools/dotnet-publish#options) 옵션에 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-162">Use the [-o|--output](/dotnet/core/tools/dotnet-publish#options) option with a path to publish to a folder outside of the app.</span></span>

### <a name="publish-a-framework-dependent-deployment-fdd"></a><span data-ttu-id="5b8f3-163">FDD(프레임워크 종속 배포) 게시</span><span class="sxs-lookup"><span data-stu-id="5b8f3-163">Publish a Framework-dependent Deployment (FDD)</span></span>

<span data-ttu-id="5b8f3-164">다음 예제에서는 앱이 *c:\\svc* 폴더에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-164">In the following example, the app is published to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --output c:\svc
```

### <a name="publish-a-self-contained-deployment-scd"></a><span data-ttu-id="5b8f3-165">SCD(자체 포함 배포) 게시</span><span class="sxs-lookup"><span data-stu-id="5b8f3-165">Publish a Self-contained Deployment (SCD)</span></span>

<span data-ttu-id="5b8f3-166">프로젝트 파일의 `<RuntimeIdenfifier>`(또는 `<RuntimeIdentifiers>`) 속성에 RID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-166">The RID must be specified in the `<RuntimeIdenfifier>` (or `<RuntimeIdentifiers>`) property of the project file.</span></span> <span data-ttu-id="5b8f3-167">`dotnet publish` 명령의 [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) 옵션에 런타임을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-167">Supply the runtime to the [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) option of the `dotnet publish` command.</span></span>

<span data-ttu-id="5b8f3-168">다음 예제에서는 앱이 `win7-x64` 런타임의 *c:\\svc* 폴더에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-168">In the following example, the app is published for the `win7-x64` runtime to the *c:\\svc* folder:</span></span>

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

## <a name="create-a-user-account"></a><span data-ttu-id="5b8f3-169">사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="5b8f3-169">Create a user account</span></span>

<span data-ttu-id="5b8f3-170">관리 PowerShell 6 명령 셸에서 `net user` 명령을 사용하여 서비스에 대한 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-170">Create a user account for the service using the `net user` command from an administrative PowerShell 6 command shell:</span></span>

```powershell
net user {USER ACCOUNT} {PASSWORD} /add
```

<span data-ttu-id="5b8f3-171">기본 암호 만료는 6주입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-171">The default password expiration is six weeks.</span></span>

<span data-ttu-id="5b8f3-172">샘플 앱의 경우, 이름이 `ServiceUser`인 사용자 계정과 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-172">For the sample app, create a user account with the name `ServiceUser` and a password.</span></span> <span data-ttu-id="5b8f3-173">다음 명령에서 `{PASSWORD}`를 [강력한 암호](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-173">In the following command, replace `{PASSWORD}` with a [strong password](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements).</span></span>

```powershell
net user ServiceUser {PASSWORD} /add
```

<span data-ttu-id="5b8f3-174">그룹에 사용자를 추가해야 하는 경우 `net localgroup` 명령을 사용합니다. 여기서 `{GROUP}`은 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-174">If you need to add the user to a group, use the `net localgroup` command, where `{GROUP}` is the name of the group:</span></span>

```powershell
net localgroup {GROUP} {USER ACCOUNT} /add
```

<span data-ttu-id="5b8f3-175">자세한 내용은 [서비스 사용자 계정](/windows/desktop/services/service-user-accounts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-175">For more information, see [Service User Accounts](/windows/desktop/services/service-user-accounts).</span></span>

<span data-ttu-id="5b8f3-176">Active Directory를 사용할 때 사용자를 관리하는 대체 방법은 관리 서비스 계정을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-176">An alternative approach to managing users when using Active Directory is to use Managed Service Accounts.</span></span> <span data-ttu-id="5b8f3-177">자세한 내용은 [그룹 관리 서비스 계정 개요](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-177">For more information, see [Group Managed Service Accounts Overview](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).</span></span>

## <a name="set-permission-log-on-as-a-service"></a><span data-ttu-id="5b8f3-178">사용 권한 설정: 서비스로 로그온</span><span class="sxs-lookup"><span data-stu-id="5b8f3-178">Set permission: Log on as a service</span></span>

<span data-ttu-id="5b8f3-179">[icacls](/windows-server/administration/windows-commands/icacls) 명령을 사용하여 앱의 폴더에 쓰기/읽기/실행 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-179">Grant write/read/execute access to the app's folder using the [icacls](/windows-server/administration/windows-commands/icacls) command:</span></span>

```powershell
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* <span data-ttu-id="5b8f3-180">`{PATH}` &ndash; 앱의 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-180">`{PATH}` &ndash; Path to the app's folder.</span></span>
* <span data-ttu-id="5b8f3-181">`{USER ACCOUNT}` &ndash; 사용자 계정(SID)입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-181">`{USER ACCOUNT}` &ndash; The user account (SID).</span></span>
* <span data-ttu-id="5b8f3-182">`(OI)` &ndash; 개체 상속 플래그는 권한을 하위 파일에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-182">`(OI)` &ndash; The Object Inherit flag propagates permissions to subordinate files.</span></span>
* <span data-ttu-id="5b8f3-183">`(CI)` &ndash; 컨테이너 상속 플래그는 권한을 하위 폴더에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-183">`(CI)` &ndash; The Container Inherit flag propagates permissions to subordinate folders.</span></span>
* <span data-ttu-id="5b8f3-184">`{PERMISSION FLAGS}` &ndash; 앱의 액세스 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-184">`{PERMISSION FLAGS}` &ndash; Sets the app's access permissions.</span></span>
  * <span data-ttu-id="5b8f3-185">쓰기(`W`)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-185">Write (`W`)</span></span>
  * <span data-ttu-id="5b8f3-186">읽기(`R`)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-186">Read (`R`)</span></span>
  * <span data-ttu-id="5b8f3-187">실행(`X`)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-187">Execute (`X`)</span></span>
  * <span data-ttu-id="5b8f3-188">전체(`F`)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-188">Full (`F`)</span></span>
  * <span data-ttu-id="5b8f3-189">수정(`M`)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-189">Modify (`M`)</span></span>
* <span data-ttu-id="5b8f3-190">`/t` &ndash; 기존 하위 폴더 및 파일에 재귀적으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-190">`/t` &ndash; Apply recursively to existing subordinate folders and files.</span></span>

<span data-ttu-id="5b8f3-191">*c:\\svc* 폴더에 게시된 샘플 앱과 쓰기/읽기/실행 권한이 있는 `ServiceUser` 계정의 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-191">For the sample app published to the *c:\\svc* folder and the `ServiceUser` account with write/read/execute permissions, use the following command:</span></span>

```powershell
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

<span data-ttu-id="5b8f3-192">자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-192">For more information, see [icacls](/windows-server/administration/windows-commands/icacls).</span></span>

## <a name="create-the-service"></a><span data-ttu-id="5b8f3-193">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5b8f3-193">Create the service</span></span>

<span data-ttu-id="5b8f3-194">[RegisterService.ps1](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/scripts) PowerShell 스크립트를 사용하여 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-194">Use the [RegisterService.ps1](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/scripts) PowerShell script to register the service.</span></span> <span data-ttu-id="5b8f3-195">관리 PowerShell 6 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-195">From an administrative PowerShell 6 command prompt, execute the following command:</span></span>

```powershell
.\RegisterService.ps1 
    -Name {NAME} 
    -DisplayName "{DISPLAY NAME}" 
    -Description "{DESCRIPTION}" 
    -Path "{PATH}" 
    -Exe {ASSEMBLY}.exe 
    -User {DOMAIN\USER}
```

<span data-ttu-id="5b8f3-196">샘플 앱에 대한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-196">In the following example for the sample app:</span></span>

* <span data-ttu-id="5b8f3-197">서비스의 이름은 **MyService**입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-197">The service is named **MyService**.</span></span>
* <span data-ttu-id="5b8f3-198">게시된 서비스는 *c:\\svc* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-198">The published service resides in the *c:\\svc* folder.</span></span> <span data-ttu-id="5b8f3-199">앱 실행 파일의 이름은 *SampleApp.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-199">The app executable is named *SampleApp.exe*.</span></span>
* <span data-ttu-id="5b8f3-200">서비스는 `ServiceUser` 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-200">The service runs under the `ServiceUser` account.</span></span> <span data-ttu-id="5b8f3-201">다음 예제에서 로컬 머신 이름은 `Desktop-PC`입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-201">In the following example, the local machine name is `Desktop-PC`.</span></span>

```powershell
.\RegisterService.ps1 
    -Name MyService 
    -DisplayName "My Cool Service" 
    -Description "This is the Sample App service." 
    -Path "c:\svc" 
    -Exe SampleApp.exe 
    -User Desktop-PC\ServiceUser
```

## <a name="manage-the-service"></a><span data-ttu-id="5b8f3-202">서비스 관리</span><span class="sxs-lookup"><span data-stu-id="5b8f3-202">Manage the service</span></span>

### <a name="start-the-service"></a><span data-ttu-id="5b8f3-203">서비스 시작</span><span class="sxs-lookup"><span data-stu-id="5b8f3-203">Start the service</span></span>

<span data-ttu-id="5b8f3-204">`Start-Service -Name {NAME}` PowerShell 6 명령을 사용하여 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-204">Start the service with the `Start-Service -Name {NAME}` PowerShell 6 command.</span></span>

<span data-ttu-id="5b8f3-205">샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-205">To start the sample app service, use the following command:</span></span>

```powershell
Start-Service -Name MyService
```

<span data-ttu-id="5b8f3-206">명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-206">The command takes a few seconds to start the service.</span></span>

### <a name="determine-the-service-status"></a><span data-ttu-id="5b8f3-207">서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="5b8f3-207">Determine the service status</span></span>

<span data-ttu-id="5b8f3-208">서비스 상태를 확인하려면 `Get-Service -Name {NAME}` PowerShell 6 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-208">To check the status of the service, use the `Get-Service -Name {NAME}` PowerShell 6 command.</span></span> <span data-ttu-id="5b8f3-209">상태는 다음 값 중 하나로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-209">The status is reported as one of the following values:</span></span>

* `Starting`
* `Running`
* `Stopping`
* `Stopped`

<span data-ttu-id="5b8f3-210">다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-210">Use the following command to check the status of the sample app service:</span></span>

```powershell
Get-Service -Name MyService
```

### <a name="browse-a-web-app-service"></a><span data-ttu-id="5b8f3-211">웹앱 서비스 찾아보기</span><span class="sxs-lookup"><span data-stu-id="5b8f3-211">Browse a web app service</span></span>

<span data-ttu-id="5b8f3-212">이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).</span><span class="sxs-lookup"><span data-stu-id="5b8f3-212">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

<span data-ttu-id="5b8f3-213">샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-213">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

### <a name="stop-the-service"></a><span data-ttu-id="5b8f3-214">서비스를 중지하여</span><span class="sxs-lookup"><span data-stu-id="5b8f3-214">Stop the service</span></span>

<span data-ttu-id="5b8f3-215">`Stop-Service -Name {NAME}` Powershell 6 명령을 사용하여 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-215">Stop the service with the `Stop-Service -Name {NAME}` Powershell 6 command.</span></span>

<span data-ttu-id="5b8f3-216">다음 명령은 샘플 앱 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-216">The following command stops the sample app service:</span></span>

```powershell
Stop-Service -Name MyService
```

### <a name="remove-the-service"></a><span data-ttu-id="5b8f3-217">서비스 제거</span><span class="sxs-lookup"><span data-stu-id="5b8f3-217">Remove the service</span></span>

<span data-ttu-id="5b8f3-218">서비스를 중지하는 짧은 지연 후에 `Remove-Service -Name {NAME}` Powershell 6 명령을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-218">After a short delay to stop a service, remove the service with the `Remove-Service -Name {NAME}` Powershell 6 command.</span></span>

<span data-ttu-id="5b8f3-219">샘플 앱 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-219">Check the status of the sample app service:</span></span>

```powershell
Remove-Service -Name MyService
```

## <a name="handle-starting-and-stopping-events"></a><span data-ttu-id="5b8f3-220">시작 및 중지 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="5b8f3-220">Handle starting and stopping events</span></span>

<span data-ttu-id="5b8f3-221"><xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*> 및 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> 이벤트를 처리하려면 추가로 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-221">To handle <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*>, and <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> events, perform the following additional changes:</span></span>

1. <span data-ttu-id="5b8f3-222">`OnStarting`, `OnStarted` 및 `OnStopping` 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService>에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-222">Create a class that derives from <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService> with the `OnStarting`, `OnStarted`, and `OnStopping` methods:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. <span data-ttu-id="5b8f3-223">`CustomWebHostService`를 <xref:System.ServiceProcess.ServiceBase.Run*>에 전달하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost>에 대한 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-223">Create an extension method for <xref:Microsoft.AspNetCore.Hosting.IWebHost> that passes the `CustomWebHostService` to <xref:System.ServiceProcess.ServiceBase.Run*>:</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="5b8f3-224">`Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> 대신 `RunAsCustomService` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-224">In `Program.Main`, call the `RunAsCustomService` extension method instead of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>:</span></span>

   ```csharp
   host.RunAsCustomService();
   ```

   <span data-ttu-id="5b8f3-225">`Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>의 위치를 확인하려면 [프로젝트를 Windows 서비스로 변환](#convert-a-project-into-a-windows-service) 섹션에 표시된 코드 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-225">To see the location of <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> in `Program.Main`, refer to the code sample shown in the [Convert a project into a Windows Service](#convert-a-project-into-a-windows-service) section.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="5b8f3-226">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="5b8f3-226">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="5b8f3-227">인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-227">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="5b8f3-228">자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-228">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="configure-https"></a><span data-ttu-id="5b8f3-229">HTTPS 구성</span><span class="sxs-lookup"><span data-stu-id="5b8f3-229">Configure HTTPS</span></span>

<span data-ttu-id="5b8f3-230">보안 엔드포인트로 서비스를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-230">To configure the service with a secure endpoint:</span></span>

1. <span data-ttu-id="5b8f3-231">플랫폼의 인증서 획득 및 배포 메커니즘을 사용하여 호스팅 시스템에 대한 X.509 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-231">Create an X.509 certificate for the hosting system using your platform's certificate acquisition and deployment mechanisms.</span></span>

1. <span data-ttu-id="5b8f3-232">[Kestrel 서버 HTTPS 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 지정하여 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-232">Specify a [Kestrel server HTTPS endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) to use the certificate.</span></span>

<span data-ttu-id="5b8f3-233">서비스 엔드포인트를 보호하기 위해 ASP.NET Core HTTPS 개발 인증서 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-233">Use of the ASP.NET Core HTTPS development certificate to secure a service endpoint isn't supported.</span></span>

## <a name="current-directory-and-content-root"></a><span data-ttu-id="5b8f3-234">현재 디렉터리 및 콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="5b8f3-234">Current directory and content root</span></span>

<span data-ttu-id="5b8f3-235">Windows 서비스에 대해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하여 반환된 현재 작업 디렉터리는 *C:\\WINDOWS\\system32* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-235">The current working directory returned by calling <xref:System.IO.Directory.GetCurrentDirectory*> for a Windows Service is the *C:\\WINDOWS\\system32* folder.</span></span> <span data-ttu-id="5b8f3-236">*system32* 폴더는 서비스의 파일(예: 설정 파일)을 저장을 저장하는 데 적절한 위치가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-236">The *system32* folder isn't a suitable location to store a service's files (for example, settings files).</span></span> <span data-ttu-id="5b8f3-237">다음 방법 중 하나를 사용하여 서비스의 자산 및 설정 파일을 유지 관리하고 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-237">Use one of the following approaches to maintain and access a service's assets and settings files.</span></span>

### <a name="set-the-content-root-path-to-the-apps-folder"></a><span data-ttu-id="5b8f3-238">콘텐츠 루트 경로를 앱 폴더로 설정</span><span class="sxs-lookup"><span data-stu-id="5b8f3-238">Set the content root path to the app's folder</span></span>

<span data-ttu-id="5b8f3-239"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*>는 서비스가 만들어질 때 `binPath` 인수에 제공된 동일한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-239">The <xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> is the same path provided to the `binPath` argument when the service is created.</span></span> <span data-ttu-id="5b8f3-240">`GetCurrentDirectory`를 호출하여 설정 파일의 경로를 만드는 대신, 앱의 콘텐츠 루트 경로를 사용하여 <xref:System.IO.Directory.SetCurrentDirectory*>를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-240">Instead of calling `GetCurrentDirectory` to create paths to settings files, call <xref:System.IO.Directory.SetCurrentDirectory*> with the path to the app's content root.</span></span>

<span data-ttu-id="5b8f3-241">`Program.Main`에서 서비스 실행 파일의 폴더 경로를 확인하고 이 경로를 사용하여 앱의 콘텐츠 루트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-241">In `Program.Main`, determine the path to the folder of the service's executable and use the path to establish the app's content root:</span></span>

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a><span data-ttu-id="5b8f3-242">디스크의 적합한 위치에 서비스 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-242">Store the service's files in a suitable location on disk</span></span>

<span data-ttu-id="5b8f3-243">파일이 포함된 폴더로 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>를 사용하는 경우 <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>를 통해 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b8f3-243">Specify an absolute path with <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> when using an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to the folder containing the files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b8f3-244">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5b8f3-244">Additional resources</span></span>

* <span data-ttu-id="5b8f3-245">[Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)(HTTPS 구성 및 SNI 지원 포함)</span><span class="sxs-lookup"><span data-stu-id="5b8f3-245">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>
