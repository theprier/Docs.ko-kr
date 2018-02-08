---
title: "ASP.NET Core에서 WebListener 웹 서버 구현"
author: rick-anderson
description: "Windows의 ASP.NET Core에 대한 웹 서버인, WebListener를 소개합니다. Http.Sys 커널 모드 드라이버를 기반으로 한 WebListener는 IIS 없이 인터넷에 대한 직접 연결에 사용될 수 있는 Kestrel에 대한 대안입니다."
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/weblistener
ms.openlocfilehash: fb2e0621645a48f4e603d754d8babbc07a78cae4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="weblistener-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="46f9a-104">ASP.NET Core에서 WebListener 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="46f9a-104">WebListener web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="46f9a-105">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="46f9a-105">By [Tom Dykstra](https://github.com/tdykstra) and [Chris Ross](https://github.com/Tratcher)</span></span>

> [!NOTE]
> <span data-ttu-id="46f9a-106">이 주제는 ASP.NET Core 1.x에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-106">This topic applies only to ASP.NET Core 1.x.</span></span> <span data-ttu-id="46f9a-107">ASP.NET Core 2.0에서는 WebListener의 이름이 [HTTP.sys](httpsys.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-107">In ASP.NET Core 2.0, WebListener is named [HTTP.sys](httpsys.md).</span></span>

<span data-ttu-id="46f9a-108">WebListener는 Windows에서만 실행되는 [ASP.NET Core에 대한 웹 서버](index.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-108">WebListener is a [web server for ASP.NET Core](index.md) that runs only on Windows.</span></span> <span data-ttu-id="46f9a-109">[Http.Sys 커널 모드 드라이버](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-109">It's built on the [Http.Sys kernel mode driver](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="46f9a-110">WebListener는 역방향 프록시 서버로 IIS를 사용하지 않고 인터넷에 대한 직접 연결에 사용될 수 있는 [Kestrel](kestrel.md)에 대한 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-110">WebListener is an alternative to [Kestrel](kestrel.md) that can be used for direct connection to the Internet without relying on IIS as a reverse proxy server.</span></span> <span data-ttu-id="46f9a-111">사실상 **WebListener는 [ASP.NET Core 모듈](aspnet-core-module.md)과 호환되지 않으므로 IIS 또는 IIS Express와 함께 사용될 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="46f9a-111">In fact, **WebListener can't be used with IIS or IIS Express, as it isn't compatible with the [ASP.NET Core Module](aspnet-core-module.md).**</span></span>

<span data-ttu-id="46f9a-112">WebListener는 ASP.NET Core에 대해 개발되었지만 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지를 통해 모든 .NET Core 또는 .NET Framework 응용 프로그램에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-112">Although WebListener was developed for ASP.NET Core, it can be used directly in any .NET Core or .NET Framework application via the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

<span data-ttu-id="46f9a-113">WebListener는 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-113">WebListener supports the following features:</span></span>

- [<span data-ttu-id="46f9a-114">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="46f9a-114">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
- <span data-ttu-id="46f9a-115">포트 공유</span><span class="sxs-lookup"><span data-stu-id="46f9a-115">Port sharing</span></span>
- <span data-ttu-id="46f9a-116">SNI로 HTTPS</span><span class="sxs-lookup"><span data-stu-id="46f9a-116">HTTPS with SNI</span></span>
- <span data-ttu-id="46f9a-117">TLS를 통한 HTTP/2(Windows 10)</span><span class="sxs-lookup"><span data-stu-id="46f9a-117">HTTP/2 over TLS (Windows 10)</span></span>
- <span data-ttu-id="46f9a-118">직접 파일 전송</span><span class="sxs-lookup"><span data-stu-id="46f9a-118">Direct file transmission</span></span>
- <span data-ttu-id="46f9a-119">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="46f9a-119">Response caching</span></span>
- <span data-ttu-id="46f9a-120">WebSocket(Windows 8)</span><span class="sxs-lookup"><span data-stu-id="46f9a-120">WebSockets (Windows 8)</span></span>

<span data-ttu-id="46f9a-121">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="46f9a-121">Supported Windows versions:</span></span>

- <span data-ttu-id="46f9a-122">Windows 7 및 Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="46f9a-122">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="46f9a-123">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="46f9a-123">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-weblistener"></a><span data-ttu-id="46f9a-124">WebListener를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="46f9a-124">When to use WebListener</span></span>

<span data-ttu-id="46f9a-125">WebListener는 IIS를 사용하지 않고 인터넷에 서버를 직접 노출해야 하는 배포에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-125">WebListener is useful for deployments where you need to expose the server directly to the Internet without using IIS.</span></span>

![WebListener는 인터넷과 직접 통신합니다.](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="46f9a-127">Http.Sys를 기반으로 하기 때문에 WebListener는 공격으로부터 보호하기 위한 역방향 프록시 서버가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-127">Because it's built on Http.Sys, WebListener doesn't require a reverse proxy server for protection against attacks.</span></span> <span data-ttu-id="46f9a-128">Http.Sys는 많은 유형의 공격으로부터 보호하고 모든 기능을 갖춘 웹 서버의 견고성, 보안 및 확장성을 제공하는 완성도 높은 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-128">Http.Sys is mature technology that protects against many kinds of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="46f9a-129">IIS 자체는 Http.Sys 위에 HTTP 수신기로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-129">IIS itself runs as an HTTP listener on top of Http.Sys.</span></span> 

<span data-ttu-id="46f9a-130">WebListener는 Kestrel을 사용하여 가져올 수 없는 제공하는 기능 중 하나가 필요할 때 내부 배포에 대한 적합한 선택이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-130">WebListener is also a good choice for internal deployments when you need one of the features it offers that you can't get by using Kestrel.</span></span>

![WebListener는 내부 네트워크와 직접 통신합니다.](weblistener/_static/weblistener-to-internal.png)

## <a name="how-to-use-weblistener"></a><span data-ttu-id="46f9a-132">WebListener 사용 방법</span><span class="sxs-lookup"><span data-stu-id="46f9a-132">How to use WebListener</span></span>

<span data-ttu-id="46f9a-133">호스트 OS 및 ASP.NET Core 응용 프로그램에 대한 설치 작업의 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-133">Here's an overview of setup tasks for the host OS and your ASP.NET Core application.</span></span>

### <a name="configure-windows-server"></a><span data-ttu-id="46f9a-134">Windows Server 구성</span><span class="sxs-lookup"><span data-stu-id="46f9a-134">Configure Windows Server</span></span>

* <span data-ttu-id="46f9a-135">[.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) 또는 .NET Framework 4.5.1과 같은 응용 프로그램에 필요한 .NET 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-135">Install the version of .NET that your application requires, such as [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) or .NET Framework 4.5.1.</span></span>

* <span data-ttu-id="46f9a-136">WebListener에 대해 바인딩하고 SSL 인증서를 설정하도록 URL 접두사 미리 등록</span><span class="sxs-lookup"><span data-stu-id="46f9a-136">Preregister URL prefixes to bind to WebListener, and set up SSL certificates</span></span>

   <span data-ttu-id="46f9a-137">Windows에서 URL 접두사를 미리 등록하지 않는 경우 관리자 권한으로 응용 프로그램을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-137">If you don't preregister URL prefixes in Windows, you have to run your application with administrator privileges.</span></span> <span data-ttu-id="46f9a-138">유일한 예외는 1024보다 큰 포트 번호로 HTTP(HTTPS 아님)를 사용하여 로컬 호스트에 바인딩하는 경우이며 이 경우 관리자 권한이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-138">The only exception is if you bind to localhost using HTTP (not HTTPS) with a port number greater than 1024; in that case administrator privileges aren't required.</span></span>

   <span data-ttu-id="46f9a-139">자세한 내용은 이 문서의 뒷부분에 나오는 [접두사 미리 등록 및 SSL 구성 방법](#preregister-url-prefixes-and-configure-ssl)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f9a-139">For details, see [How to preregister prefixes and configure SSL](#preregister-url-prefixes-and-configure-ssl) later in this article.</span></span>

* <span data-ttu-id="46f9a-140">방화벽 포트를 열어 WebListener에 도달하는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-140">Open firewall ports to allow traffic to reach WebListener.</span></span>

   <span data-ttu-id="46f9a-141">netsh.exe 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-141">You can use netsh.exe or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

<span data-ttu-id="46f9a-142">[Http.Sys 레지스트리 설정](https://support.microsoft.com/kb/820129)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-142">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>

### <a name="configure-your-aspnet-core-application"></a><span data-ttu-id="46f9a-143">ASP.NET Core 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="46f9a-143">Configure your ASP.NET Core application</span></span>

* <span data-ttu-id="46f9a-144">NuGet 패키지 [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-144">Install the NuGet package [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/).</span></span> <span data-ttu-id="46f9a-145">종속성으로 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/)도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-145">This also installs [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) as a dependency.</span></span>

* <span data-ttu-id="46f9a-146">다음 예제와 같이 필요한 WebListener [옵션](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) 및 [설정](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs)을 지정하여 `Main` 메서드에서 [WebHostBuilder](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder)의 `UseWebListener` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-146">Call the `UseWebListener` extension method on [WebHostBuilder](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) in your `Main` method, specifying any WebListener [options](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) and [settings](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs) that you need, as shown in the following example:</span></span>

  [!code-csharp[](weblistener/sample/Program.cs?name=snippet_Main&highlight=13-17)]

* <span data-ttu-id="46f9a-147">수신 대기하는 URL 및 포트 구성</span><span class="sxs-lookup"><span data-stu-id="46f9a-147">Configure URLs and ports to listen on</span></span> 

  <span data-ttu-id="46f9a-148">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-148">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="46f9a-149">URL 접두사와 포트를 구성하기 위해 `UseURLs` 확장 메서드, `urls` 명령줄 인수 또는 ASP.NET Core 구성 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-149">To configure URL prefixes and ports, you can use the `UseURLs` extension method, the `urls` command-line argument or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="46f9a-150">자세한 내용은 [호스팅](../../fundamentals/hosting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f9a-150">For more information, see [Hosting](../../fundamentals/hosting.md).</span></span>

  <span data-ttu-id="46f9a-151">웹 수신기는 [Http.Sys 접두사 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-151">Web Listener uses the [Http.Sys prefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span> <span data-ttu-id="46f9a-152">WebListener와 관련된 접두사 문자열 형식 요구 사항이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-152">There are no prefix string format requirements that are specific to WebListener.</span></span>

  > [!NOTE]
  > <span data-ttu-id="46f9a-153">서버에서 미리 등록한 동일한 접두사 문자열을 `UseUrls`에 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-153">Make sure that you specify the same prefix strings in `UseUrls` that you preregister on the server.</span></span> 

* <span data-ttu-id="46f9a-154">응용 프로그램은 IIS 또는 IIS Express를 실행하도록 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-154">Make sure your application isn't configured to run IIS or IIS Express.</span></span>

  <span data-ttu-id="46f9a-155">Visual Studio에서 기본 실행 프로필은 IIS Express용입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-155">In Visual Studio, the default launch profile is for IIS Express.</span></span>  <span data-ttu-id="46f9a-156">콘솔 응용 프로그램으로 프로젝트를 실행하려면 다음 스크린샷에 표시된 것처럼 수동으로 선택한 프로필을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-156">To run the project as a console application you have to manually change the selected profile, as shown in the following screen shot.</span></span>

  ![콘솔 앱 프로필 선택](weblistener/_static/vs-choose-profile.png)

## <a name="how-to-use-weblistener-outside-of-aspnet-core"></a><span data-ttu-id="46f9a-158">ASP.NET Core 외부에서 WebListener를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="46f9a-158">How to use WebListener outside of ASP.NET Core</span></span>

* <span data-ttu-id="46f9a-159">[Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-159">Install the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

* <span data-ttu-id="46f9a-160">ASP.NET Core에서 사용을 위해 수행하는 것처럼 [WebListener에 대해 바인딩하고 SSL 인증서를 설정하도록 URL 접두사 미리 등록합니다](#preregister-url-prefixes-and-configure-ssl).</span><span class="sxs-lookup"><span data-stu-id="46f9a-160">[Preregister URL prefixes to bind to WebListener, and set up SSL certificates](#preregister-url-prefixes-and-configure-ssl) as you would for use in ASP.NET Core.</span></span>

<span data-ttu-id="46f9a-161">[Http.Sys 레지스트리 설정](https://support.microsoft.com/kb/820129)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-161">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>


<span data-ttu-id="46f9a-162">ASP.NET Core 외부에서 WebListener 사용을 보여 주는 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-162">Here's a code sample that demonstrates WebListener use outside of ASP.NET Core:</span></span>

```csharp
var settings = new WebListenerSettings();
settings.UrlPrefixes.Add("http://localhost:8080");

using (WebListener listener = new WebListener(settings))
{
    listener.Start();

    while (true)
    {
        var context = await listener.AcceptAsync();
        byte[] bytes = Encoding.ASCII.GetBytes("Hello World: " + DateTime.Now);
        context.Response.ContentLength = bytes.Length;
        context.Response.ContentType = "text/plain";

        await context.Response.Body.WriteAsync(bytes, 0, bytes.Length);
        context.Dispose();
    }
}
```

## <a name="preregister-url-prefixes-and-configure-ssl"></a><span data-ttu-id="46f9a-163">URL 접두사 미리 등록 및 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="46f9a-163">Preregister URL prefixes and configure SSL</span></span>

<span data-ttu-id="46f9a-164">IIS와 WebListener는 기본 Http.Sys 커널 모드 드라이버를 사용하여 요청을 수신하고 초기 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-164">Both IIS and WebListener rely on the underlying Http.Sys kernel mode driver to listen for requests and do initial processing.</span></span> <span data-ttu-id="46f9a-165">IIS에서 관리 UI는 모든 항목을 구성하는 상대적으로 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-165">In IIS, the management UI gives you a relatively easy way to configure everything.</span></span> <span data-ttu-id="46f9a-166">그러나 WebListener를 사용하는 경우 Http.Sys를 직접 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-166">However, if you're using WebListener you need to configure Http.Sys yourself.</span></span> <span data-ttu-id="46f9a-167">작업 수행을 위한 기본 도구는 netsh.exe입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-167">The built-in tool for doing that's netsh.exe.</span></span> 

<span data-ttu-id="46f9a-168">netsh.exe를 사용해야 하는 가장 일반적인 작업은 URL 접두사 예약 및 SSL 인증서 할당입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-168">The most common tasks you need to use netsh.exe for are reserving URL prefixes and assigning SSL certificates.</span></span>

<span data-ttu-id="46f9a-169">NetSh.exe는 초보자가 사용하기에 편리한 도구가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-169">NetSh.exe isn't an easy tool to use for beginners.</span></span> <span data-ttu-id="46f9a-170">다음 예제에서는 포트 80 및 443에 대해 URL 접두사를 예약하는 데 필요한 최소한의 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-170">The following example shows the bare minimum needed to reserve URL prefixes for ports 80 and 443:</span></span>

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

<span data-ttu-id="46f9a-171">다음 예제에서는 SSL 인증서를 할당하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-171">The following example shows how to assign an SSL certificate:</span></span>

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}".
```

<span data-ttu-id="46f9a-172">다음은 공식 참조 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-172">Here is the official reference documentation:</span></span>

* [<span data-ttu-id="46f9a-173">HTTP(Hypertext Transfer Protocol)에 대한 Netsh 명령</span><span class="sxs-lookup"><span data-stu-id="46f9a-173">Netsh Commands for Hypertext Transfer Protocol (HTTP)</span></span>](https://technet.microsoft.com/library/cc725882.aspx)
* [<span data-ttu-id="46f9a-174">UrlPrefix 문자열</span><span class="sxs-lookup"><span data-stu-id="46f9a-174">UrlPrefix Strings</span></span>](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

<span data-ttu-id="46f9a-175">다음 리소스는 여러 시나리오에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-175">The following resources provide detailed instructions for several scenarios.</span></span> <span data-ttu-id="46f9a-176">`HttpListener`를 참조하는 문서는 모두 Http.Sys를 기반으로 하므로 `WebListener`에 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-176">Articles that refer to `HttpListener` apply equally to `WebListener`, as both are based on Http.Sys.</span></span>

* [<span data-ttu-id="46f9a-177">방법: SSL 인증서로 포트 구성</span><span class="sxs-lookup"><span data-stu-id="46f9a-177">How to: Configure a Port with an SSL Certificate</span></span>](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* <span data-ttu-id="46f9a-178">[HTTPS 통신 - HttpListener 기반 호스팅 및 클라이언트 인증](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) 이는 타사 블로그이며 비교적 오래됐지만 여전히 유용한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-178">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) This is a third-party blog and is fairly old but still has useful information.</span></span>
* <span data-ttu-id="46f9a-179">[방법: SSL 단순 서버로 HttpListener 또는 Http 서버 안전하지 않은 코드(C++)를 사용하는 연습](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) 유용한 정보가 있는 오래된 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-179">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) This too is an older blog with useful information.</span></span>
* [<span data-ttu-id="46f9a-180">SSL로 .NET Core WebListener를 어떻게 설정하나요?</span><span class="sxs-lookup"><span data-stu-id="46f9a-180">How Do I Set Up A .NET Core WebListener With SSL?</span></span>](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)

<span data-ttu-id="46f9a-181">다음은 netsh.exe 명령줄보다 쉽게 사용할 수 있는 몇 가지 타사 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-181">Here are some third-party tools that can be easier to use than the netsh.exe command line.</span></span> <span data-ttu-id="46f9a-182">이러한 도구는 Microsoft에서 제공되거나 보증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-182">These are not provided by or endorsed by Microsoft.</span></span> <span data-ttu-id="46f9a-183">netsh.exe 자체는 관리자 권한이 필요하므로 도구는 기본적으로 관리자 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-183">The tools run as administrator by default, since netsh.exe itself requires administrator privileges.</span></span>

* <span data-ttu-id="46f9a-184">[http.sys 관리자](http://httpsysmanager.codeplex.com/)는 SSL 인증서 및 옵션, 접두사 예약 및 인증서 신뢰 목록의 나열 및 구성을 위한 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-184">[http.sys Manager](http://httpsysmanager.codeplex.com/) provides UI for listing and configuring SSL certificates and options, prefix reservations, and certificate trust lists.</span></span> 
* <span data-ttu-id="46f9a-185">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx)를 통해 SSL 인증서와 URL 접두사를 나열하거나 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-185">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) lets you list or configure SSL certificates and URL prefixes.</span></span> <span data-ttu-id="46f9a-186">UI는 http.sys 관리자보다 성능이 우수하며 몇 가지 추가 구성 옵션을 노출하지만 그렇지 않은 경우 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-186">The UI is more refined than http.sys Manager and exposes a few more configuration options, but otherwise it provides similar functionality.</span></span> <span data-ttu-id="46f9a-187">새 CTL(인증서 신뢰 목록)을 만들 수 없지만 기존 것을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-187">It cannot create a new certificate trust list (CTL), but can assign existing ones.</span></span>

<span data-ttu-id="46f9a-188">자체 서명된 SSL 인증서를 생성하기 위해 Microsoft는 명령줄 도구: [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) 및 PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-188">For generating self-signed SSL certificates, Microsoft provides command-line tools: [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) and the PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate).</span></span> <span data-ttu-id="46f9a-189">자체 서명된 SSL 인증서를 쉽게 생성하도록 하는 타사 UI 도구도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f9a-189">There are also third-party UI tools that make it easier for you to generate self-signed SSL certificates:</span></span>

* [<span data-ttu-id="46f9a-190">SelfCert</span><span class="sxs-lookup"><span data-stu-id="46f9a-190">SelfCert</span></span>](https://www.pluralsight.com/blog/software-development/selfcert-create-a-self-signed-certificate-interactively-gui-or-programmatically-in-net)
* [<span data-ttu-id="46f9a-191">Makecert UI</span><span class="sxs-lookup"><span data-stu-id="46f9a-191">Makecert UI</span></span>](http://makecertui.codeplex.com/)

## <a name="next-steps"></a><span data-ttu-id="46f9a-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46f9a-192">Next steps</span></span>

<span data-ttu-id="46f9a-193">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f9a-193">For more information, see the following resources:</span></span>

* [<span data-ttu-id="46f9a-194">이 문서에 대한 샘플 앱</span><span class="sxs-lookup"><span data-stu-id="46f9a-194">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)
* [<span data-ttu-id="46f9a-195">WebListener 소스 코드</span><span class="sxs-lookup"><span data-stu-id="46f9a-195">WebListener source code</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="46f9a-196">호스팅</span><span class="sxs-lookup"><span data-stu-id="46f9a-196">Hosting</span></span>](../hosting.md)
