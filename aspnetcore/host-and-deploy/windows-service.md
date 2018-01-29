---
title: "Windows 서비스의 호스트"
author: tdykstra
description: "Windows 서비스에서 ASP.NET Core 응용 프로그램을 호스트 하는 방법을 알아봅니다."
ms.author: tdykstra
manager: wpickett
ms.custom: mvc
ms.date: 03/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: host-and-deploy/windows-service
ms.openlocfilehash: 4bf64f54dd9c6d2a1706bd405b0d6d75d7573a7a
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="host-an-aspnet-core-app-in-a-windows-service"></a><span data-ttu-id="da529-103">Windows 서비스에서 ASP.NET Core 응용 프로그램 호스트</span><span class="sxs-lookup"><span data-stu-id="da529-103">Host an ASP.NET Core app in a Windows Service</span></span>

<span data-ttu-id="da529-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="da529-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="da529-105">IIS를 사용 하 여 실행 하는 것 하지 않고 Windows에서 ASP.NET Core 응용 프로그램을 호스트 하는 권장된 방법은 [Windows 서비스](https://docs.microsoft.com/dotnet/framework/windows-services/introduction-to-windows-service-applications)합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](https://docs.microsoft.com/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="da529-106">이런 방식으로 시작할 수 있습니다 자동으로 다시 부팅 하 고 충돌 후 다른 사용자가 로그인 할 때까지 기다리지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-106">That way it can automatically start after reboots and crashes, without waiting for someone to log in.</span></span>

<span data-ttu-id="da529-107">[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="da529-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="da529-108">참조는 [다음 단계](#next-steps) 실행 하는 방법에 대 한 지침은 섹션.</span><span class="sxs-lookup"><span data-stu-id="da529-108">See the [Next Steps](#next-steps) section for instructions on how to run it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da529-109">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="da529-109">Prerequisites</span></span>

* <span data-ttu-id="da529-110">앱을.NET Framework 런타임에 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-110">The app must run on the .NET Framework runtime.</span></span>  <span data-ttu-id="da529-111">에 *.csproj* 파일,이 대 한 적절 한 값을 지정 [TargetFramework](https://docs.microsoft.com/nuget/schema/target-frameworks) 및 [RuntimeIdentifier](https://docs.microsoft.com/dotnet/articles/core/rid-catalog)합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-111">In the *.csproj* file, specify appropriate values for [TargetFramework](https://docs.microsoft.com/nuget/schema/target-frameworks) and [RuntimeIdentifier](https://docs.microsoft.com/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="da529-112">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da529-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="da529-113">Visual Studio에서 프로젝트를 만들 때 사용 된 **ASP.NET Core 응용 프로그램 (.NET Framework)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="da529-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="da529-114">사용 해야 합니다 (뿐 아니라 내부 네트워크)에서 인터넷을 통해 요청을 수신 하는 응용 프로그램을 하는 경우는 [WebListener](xref:fundamentals/servers/weblistener) 웹 서버 대신 [Kestrel](xref:fundamentals/servers/kestrel)합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-114">If the app receives requests from the Internet (not just from an internal network), it must use the [WebListener](xref:fundamentals/servers/weblistener) web server rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span>  <span data-ttu-id="da529-115">Kestrel은 가장자리 배포에 대 한 IIS 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-115">Kestrel must be used with IIS for edge deployments.</span></span>  <span data-ttu-id="da529-116">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da529-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="getting-started"></a><span data-ttu-id="da529-117">시작</span><span class="sxs-lookup"><span data-stu-id="da529-117">Getting started</span></span>

<span data-ttu-id="da529-118">이 섹션에서는 서비스에서 실행 되도록 기존 ASP.NET Core 프로젝트를 설정 하는 데 필요한 최소한의 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

* <span data-ttu-id="da529-119">NuGet 패키지 설치 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

* <span data-ttu-id="da529-120">다음과 같이 변경 `Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="da529-120">Make the following changes in `Program.Main`:</span></span>
  
  * <span data-ttu-id="da529-121">호출 `host.RunAsService` 대신 `host.Run`합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-121">Call `host.RunAsService` instead of `host.Run`.</span></span>
  
  * <span data-ttu-id="da529-122">코드에서 호출 하는 경우 `UseContentRoot`, 대신 게시 위치에 경로 사용 합니다.`Directory.GetCurrentDirectory()`</span><span class="sxs-lookup"><span data-stu-id="da529-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`</span></span> 
  
  [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

* <span data-ttu-id="da529-123">폴더에 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-123">Publish the application to a folder.</span></span>

  <span data-ttu-id="da529-124">사용 하 여 [dotnet 게시](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-publish) 또는 [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 폴더에 게시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-124">Use [dotnet publish](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

* <span data-ttu-id="da529-125">만들고 서비스를 시작 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-125">Test by creating and starting the service.</span></span>

  <span data-ttu-id="da529-126">사용 하려면 관리자 명령 프롬프트 창을 엽니다는 [sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 만들고 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-126">Open an administrator command prompt window to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span>  
  
  <span data-ttu-id="da529-127">MyService 서비스에 이름이 인 경우에 앱을 게시 `c:\svc`, 및 앱 자체가 AspNetCoreService 라는, 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da529-127">If the service is named MyService, publish the app to `c:\svc`, and the app itself is named AspNetCoreService, the commands would look like this:</span></span>

  ```console
  sc create MyService binPath="C:\Svc\AspNetCoreService.exe"
  sc start MyService
  ```

  <span data-ttu-id="da529-128">`binPath` 값은 실행 파일 이름 자체를 포함 하 여 응용 프로그램의 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="da529-128">The `binPath` value is the path to the app's executable, including the executable filename itself.</span></span>

  ![콘솔 창에서 만들고 시작 예제](windows-service/_static/create-start.png)

  <span data-ttu-id="da529-130">콘솔 응용 프로그램으로 실행할 때 이러한 명령을 완료 하는 경우와 같은 경로을 찾습니다 (기본적으로 `http://localhost:5000`)</span><span class="sxs-lookup"><span data-stu-id="da529-130">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`)</span></span>

  ![서비스에서 실행](windows-service/_static/running-in-service.png)


## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="da529-132">서비스 외부에서 실행 하는 방법을 제공합니다</span><span class="sxs-lookup"><span data-stu-id="da529-132">Provide a way to run outside of a service</span></span>

<span data-ttu-id="da529-133">테스트 하 고 호출 하는 코드를 추가 하는 일반적인 것 이므로 외부 서비스를 실행 하는 경우 디버깅할 쉽게 `host.RunAsService` 특정 조건 에서만.</span><span class="sxs-lookup"><span data-stu-id="da529-133">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `host.RunAsService` only under certain conditions.</span></span>  <span data-ttu-id="da529-134">예를 들어, 응용 프로그램으로 콘솔 응용 프로그램으로 실행할 수는 `--console` 명령줄 인수나는 디버거가 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da529-134">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached.</span></span>

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="da529-135">중지 및 시작 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-135">Handle stopping and starting events</span></span>

<span data-ttu-id="da529-136">처리 하기 `OnStarting`, `OnStarted`, 및 `OnStopping` 이벤트를 다음과 같이 변경 추가:</span><span class="sxs-lookup"><span data-stu-id="da529-136">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

* <span data-ttu-id="da529-137">`WebHostService`에서 파생되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da529-137">Create a class that derives from `WebHostService`.</span></span>

  [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

* <span data-ttu-id="da529-138">에 대 한 확장 메서드를 만들어 `IWebHost` 사용자 지정을 통과 하 `WebHostService` 를 `ServiceBase.Run`합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-138">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`.</span></span>

  [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

* <span data-ttu-id="da529-139">`Program.Main` 대신 새 확장 메서드를 호출 하는 변경 `host.RunAsService`합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-139">In `Program.Main` change call the new extension method instead of `host.RunAsService`.</span></span>

  [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=26)]

<span data-ttu-id="da529-140">하는 경우 사용자 지정 `WebHostService` 코드 (예:로 거) 종속성 주입에서 서비스 가져오기에서 발생할 해야는 `Services` 속성 `IWebHost`합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-140">If the custom `WebHostService` code needs to get a service from dependency injection (such as a logger), get it from the `Services` property of `IWebHost`.</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="next-steps"></a><span data-ttu-id="da529-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da529-141">Next steps</span></span>

<span data-ttu-id="da529-142">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) 이 함께 제공 되는 문서는 이전 코드 예제에서와 같이 수정 된 간단한 MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="da529-142">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) that accompanies this article is a simple MVC web app that has been modified as shown in preceding code examples.</span></span>  <span data-ttu-id="da529-143">도구를 서비스에서 실행 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-143">To run it in a service, do the following steps:</span></span>

* <span data-ttu-id="da529-144">에 게시 *c:\svc*합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-144">Publish to *c:\svc*.</span></span>

* <span data-ttu-id="da529-145">관리자 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da529-145">Open an administrator window.</span></span>

* <span data-ttu-id="da529-146">다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-146">Enter the following commands:</span></span>

  ```console
  sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
  sc start MyService
  ```

  * <span data-ttu-id="da529-147">브라우저에서 실행 중인지 확인 http://localhost:5000 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-147">In a browser, go to http://localhost:5000 to verify that it's running.</span></span>

<span data-ttu-id="da529-148">오류 메시지에 액세스할 수 있도록 하는 빠른 방법을 같은 로깅 공급자를 추가 하는 응용 프로그램은 서비스에서 실행 하는 경우 예상 대로 최대 시작 되지 않으면는 [Windows 이벤트 로그 공급자](xref:fundamentals/logging/index#eventlog)합니다.</span><span class="sxs-lookup"><span data-stu-id="da529-148">If the app doesn't start up as expected when running in a service, a quick way to make error messages accessible is to add a logging provider such as the [Windows EventLog provider](xref:fundamentals/logging/index#eventlog).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="da529-149">승인</span><span class="sxs-lookup"><span data-stu-id="da529-149">Acknowledgments</span></span>

<span data-ttu-id="da529-150">이미 게시 된 원본의 도움을 받아가이 문서의 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="da529-150">This article was written with the help of sources that were already published.</span></span> <span data-ttu-id="da529-151">시작와 그 중 가장 유용한 이러한 다음과 같았습니다.</span><span class="sxs-lookup"><span data-stu-id="da529-151">The earliest and most useful of them were these:</span></span>

* [<span data-ttu-id="da529-152">ASP.NET Core Windows 서비스 호스팅</span><span class="sxs-lookup"><span data-stu-id="da529-152">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="da529-153">Windows 서비스에서 ASP.NET Core 프로그램을 호스트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="da529-153">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
