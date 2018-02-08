---
title: "ASP.NET Core에서 HTTP.sys 웹 서버 구현"
author: rick-anderson
description: "Windows의 ASP.NET Core에 대한 웹 서버인, HTTP.sys를 소개합니다. Http.Sys 커널 모드 드라이버를 기반으로 한 HTTP.sys는 IIS 없이 인터넷에 대한 직접 연결에 사용될 수 있는 Kestrel에 대한 대안입니다."
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: f36a86fc67e715165afd0c38992f9767f90cf3b4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="2821f-104">ASP.NET Core에서 HTTP.sys 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="2821f-104">HTTP.sys web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="2821f-105">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="2821f-105">By [Tom Dykstra](https://github.com/tdykstra) and [Chris Ross](https://github.com/Tratcher)</span></span>

> [!NOTE]
> <span data-ttu-id="2821f-106">이 주제는 ASP.NET Core 2.0 이상에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-106">This topic applies only to ASP.NET Core 2.0 and later.</span></span> <span data-ttu-id="2821f-107">이전 버전의 ASP.NET Core에서 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-107">In earlier versions of ASP.NET Core, HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener).</span></span>

<span data-ttu-id="2821f-108">HTTP.sys는 Windows에서만 실행되는 [ASP.NET Core에 대한 웹 서버](index.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-108">HTTP.sys is a [web server for ASP.NET Core](index.md) that runs only on Windows.</span></span> <span data-ttu-id="2821f-109">[Http.Sys 커널 모드 드라이버](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-109">It's built on the [Http.Sys kernel mode driver](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="2821f-110">HTTP.sys는 Kestel이 하지 않는 일부 기능을 제공하는 [Kestrel](kestrel.md)에 대한 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-110">HTTP.sys is an alternative to [Kestrel](kestrel.md) that offers some features that Kestel doesn't.</span></span> <span data-ttu-id="2821f-111">**HTTP.sys는 [ASP.NET Core 모듈](aspnet-core-module.md)과 호환되지 않으므로 IIS 또는 IIS Express와 함께 사용될 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="2821f-111">**HTTP.sys can't be used with IIS or IIS Express, as it's incompatible with the [ASP.NET Core Module](aspnet-core-module.md).**</span></span>

<span data-ttu-id="2821f-112">HTTP.sys는 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-112">HTTP.sys supports the following features:</span></span>

- [<span data-ttu-id="2821f-113">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="2821f-113">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
- <span data-ttu-id="2821f-114">포트 공유</span><span class="sxs-lookup"><span data-stu-id="2821f-114">Port sharing</span></span>
- <span data-ttu-id="2821f-115">SNI를 사용하는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="2821f-115">HTTPS with SNI</span></span>
- <span data-ttu-id="2821f-116">TLS를 통한 HTTP/2(Windows 10)</span><span class="sxs-lookup"><span data-stu-id="2821f-116">HTTP/2 over TLS (Windows 10)</span></span>
- <span data-ttu-id="2821f-117">직접 파일 전송</span><span class="sxs-lookup"><span data-stu-id="2821f-117">Direct file transmission</span></span>
- <span data-ttu-id="2821f-118">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="2821f-118">Response caching</span></span>
- <span data-ttu-id="2821f-119">WebSockets(Windows 8)</span><span class="sxs-lookup"><span data-stu-id="2821f-119">WebSockets (Windows 8)</span></span>

<span data-ttu-id="2821f-120">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="2821f-120">Supported Windows versions:</span></span>

- <span data-ttu-id="2821f-121">Windows 7 및 Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="2821f-121">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="2821f-122">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="2821f-122">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-httpsys"></a><span data-ttu-id="2821f-123">HTTP.sys를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="2821f-123">When to use HTTP.sys</span></span>

<span data-ttu-id="2821f-124">HTTP.sys는 IIS를 사용하지 않고 인터넷에 서버를 직접 노출해야 하는 배포에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-124">HTTP.sys is useful for deployments where you need to expose the server directly to the Internet without using IIS.</span></span>

![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="2821f-126">Http.Sys를 기반으로 하기 때문에 HTTP.sys는 공격으로부터 보호하기 위한 역방향 프록시 서버가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-126">Because it's built on Http.Sys, HTTP.sys doesn't require a reverse proxy server for protection against attacks.</span></span> <span data-ttu-id="2821f-127">Http.Sys는 많은 유형의 공격으로부터 보호하고 모든 기능을 갖춘 웹 서버의 견고성, 보안 및 확장성을 제공하는 완성도 높은 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-127">Http.Sys is mature technology that protects against many kinds of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="2821f-128">IIS 자체는 Http.Sys 위에 HTTP 수신기로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-128">IIS itself runs as an HTTP listener on top of Http.Sys.</span></span> 

<span data-ttu-id="2821f-129">HTTP.sys는 Windows 인증과 같이 Kestrel에서 사용할 수 없는 기능이 필요한 경우 내부 배포에 적합한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-129">HTTP.sys is a good choice for internal deployments when you need a feature not available in Kestrel, such as Windows authentication.</span></span>

![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

## <a name="how-to-use-httpsys"></a><span data-ttu-id="2821f-131">HTTP.sys 사용 방법</span><span class="sxs-lookup"><span data-stu-id="2821f-131">How to use HTTP.sys</span></span>

<span data-ttu-id="2821f-132">호스트 OS 및 사용자의 ASP.NET Core 응용 프로그램에 대한 설치 작업의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-132">Here's an overview of setup tasks for the host OS and your ASP.NET Core application.</span></span>

### <a name="configure-windows-server"></a><span data-ttu-id="2821f-133">Windows Server 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-133">Configure Windows Server</span></span>

* <span data-ttu-id="2821f-134">[.NET Core](https://www.microsoft.com/net/download/core) 또는 [.NET Framework](https://www.microsoft.com/net/download/framework)와 같은 응용 프로그램에 필요한 .NET 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-134">Install the version of .NET that your application requires, such as [.NET Core](https://www.microsoft.com/net/download/core) or [.NET Framework](https://www.microsoft.com/net/download/framework).</span></span>

* <span data-ttu-id="2821f-135">HTTP.sys에 대해 바인딩하고 SSL 인증서를 설정하도록 URL 접두사 미리 등록</span><span class="sxs-lookup"><span data-stu-id="2821f-135">Preregister URL prefixes to bind to HTTP.sys, and set up SSL certificates</span></span>

   <span data-ttu-id="2821f-136">Windows에서 URL 접두사를 미리 등록하지 않은 경우 관리자 권한으로 응용 프로그램을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-136">If you don't preregister URL prefixes in Windows, you have to run your application with administrator privileges.</span></span> <span data-ttu-id="2821f-137">유일한 예외는 포트 번호가 1024보다 큰 HTTP(HTTPS 아님)를 사용하여 로컬 호스트에 바인딩하는 경우로, 이 경우 관리자 권한은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-137">The only exception is if you bind to localhost using HTTP (not HTTPS) with a port number greater than 1024; in that case, administrator privileges aren't required.</span></span>

   <span data-ttu-id="2821f-138">자세한 내용은 이 문서의 뒷부분에 나오는 [접두사를 미리 등록하고 SSL을 구성하는 방법](#preregister-url-prefixes-and-configure-ssl)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2821f-138">For details, see [How to preregister prefixes and configure SSL](#preregister-url-prefixes-and-configure-ssl) later in this article.</span></span>

* <span data-ttu-id="2821f-139">방화벽 포트를 열어 HTTP.sys에 도달하는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-139">Open firewall ports to allow traffic to reach HTTP.sys.</span></span>

   <span data-ttu-id="2821f-140">*netsh.exe* 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-140">You can use *netsh.exe* or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

<span data-ttu-id="2821f-141">[Http.Sys 레지스트리 설정](https://support.microsoft.com/kb/820129)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-141">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>

### <a name="configure-your-aspnet-core-application-to-use-httpsys"></a><span data-ttu-id="2821f-142">HTTP.sys를 사용하도록 ASP.NET Core 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-142">Configure your ASP.NET Core application to use HTTP.sys</span></span>

* <span data-ttu-id="2821f-143">[Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 메타패키지를 사용하는 경우에는 패키지를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-143">No package install is needed if you use the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage.</span></span> <span data-ttu-id="2821f-144">[Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) 패키지는 메타패키지에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-144">The [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) package is included in the metapackage.</span></span>

* <span data-ttu-id="2821f-145">다음 예제와 같이 필요한 [HTTP.sys 옵션](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)을 지정하여 `Main` 메서드에서 `WebHostBuilder`의 `UseHttpSys` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-145">Call the `UseHttpSys` extension method on `WebHostBuilder` in your `Main` method, specifying any [HTTP.sys options](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs) that you need, as shown in the following example:</span></span>

  [!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=11-19)]

### <a name="configure-httpsys-options"></a><span data-ttu-id="2821f-146">HTTP.sys 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-146">Configure HTTP.sys options</span></span>

<span data-ttu-id="2821f-147">다음은 몇 가지 구성 가능한 HTTP.sys 설정 및 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-147">Here are some of the HTTP.sys settings and limits that you can configure.</span></span>

<span data-ttu-id="2821f-148">**최대 클라이언트 연결**</span><span class="sxs-lookup"><span data-stu-id="2821f-148">**Maximum client connections**</span></span>

<span data-ttu-id="2821f-149">*Program.cs*의 다음 코드를 사용하여 전체 응용 프로그램에 대한 동시 개방 TCP 연결의 최대 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-149">The maximum number of concurrent open TCP connections can be set for the entire application with the following code in *Program.cs*:</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=5)]

<span data-ttu-id="2821f-150">연결의 최대 수는 기본적으로 무제한(null)입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-150">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="2821f-151">**최대 요청 본문 크기**</span><span class="sxs-lookup"><span data-stu-id="2821f-151">**Maximum request body size**</span></span>

<span data-ttu-id="2821f-152">기본 최대 요청 본문 크기는 약 28.6MB인 30,000,000바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-152">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span>

<span data-ttu-id="2821f-153">ASP.NET Core MVC 앱에서 한도를 재정의할 때는 작업 메서드에서 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 특성을 사용하는 방법이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-153">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="2821f-154">다음 예제는 전체 응용 프로그램, 모든 요청에 대한 제약 조건을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-154">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=6)]

<span data-ttu-id="2821f-155">*Startup.cs*에서 특정 요청에 대한 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-155">You can override the setting on a specific request in *Startup.cs*:</span></span>

[!code-csharp[](httpsys/sample/Startup.cs?name=snippet_Configure&highlight=9-10)]
 
<span data-ttu-id="2821f-156">응용 프로그램에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-156">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="2821f-157">`MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 알려주는 `IsReadOnly` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-157">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="2821f-158">다른 HTTP.sys 옵션에 대한 정보는 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2821f-158">For information about other HTTP.sys options, see [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs).</span></span> 

### <a name="configure-urls-and-ports-to-listen-on"></a><span data-ttu-id="2821f-159">수신 대기하는 URL 및 포트 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-159">Configure URLs and ports to listen on</span></span> 

<span data-ttu-id="2821f-160">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-160">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="2821f-161">URL 접두사 및 포트를 구성하려면 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)에서 `UseUrls` 확장 메서드, `urls` 명령줄 인수, ASPNETCORE_URLS 환경 변수 또는 `UrlPrefixes` 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-161">To configure URL prefixes and ports, you can use the `UseUrls` extension method, the `urls` command-line argument, the ASPNETCORE_URLS environment variable, or the `UrlPrefixes` property on [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs).</span></span> <span data-ttu-id="2821f-162">다음 코드 예제에서는 `UrlPrefixes`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-162">The following code example uses `UrlPrefixes`.</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=17)]

<span data-ttu-id="2821f-163">`UrlPrefixes`의 이점은 서식이 잘못 지정된 접두사를 추가하려고 하면 오류 메시지가 즉시 표시된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-163">An advantage of `UrlPrefixes` is that you get an error message immediately if you try to add a prefix that's formatted wrong.</span></span> <span data-ttu-id="2821f-164">`UseUrls`(`urls` 및 ASPNETCORE_URLS과 공유)의 이점은 더 쉽게 Kestrel 및 HTTP.sys 간 전환이 가능하다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-164">An advantage of `UseUrls` (shared with `urls` and ASPNETCORE_URLS) is that you can more easily switch between Kestrel and HTTP.sys.</span></span>

<span data-ttu-id="2821f-165">`UseUrls`(또는 `urls` 또는 ASPNETCORE_URLS) 및 `UrlPrefixes`를 모두 사용하는 경우 `UrlPrefixes`의 설정은 `UseUrls`의 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-165">If you use both `UseUrls` (or `urls` or ASPNETCORE_URLS) and `UrlPrefixes`, the settings in `UrlPrefixes` override the ones in `UseUrls`.</span></span> <span data-ttu-id="2821f-166">자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2821f-166">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

<span data-ttu-id="2821f-167">HTTP.sys는 [HTTP Server API UrlPrefix 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-167">HTTP.sys uses the [HTTP Server API UrlPrefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2821f-168">서버에서 미리 등록한 동일한 접두사 문자열을 `UseUrls` 또는 `UrlPrefixes`에서 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-168">Make sure that you specify the same prefix strings in `UseUrls` or `UrlPrefixes` that you preregister on the server.</span></span> 

### <a name="dont-use-iis"></a><span data-ttu-id="2821f-169">IIS 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2821f-169">Don't use IIS</span></span>

<span data-ttu-id="2821f-170">응용 프로그램이 IIS 또는 IIS Express를 실행하도록 구성되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-170">Make sure your application isn't configured to run IIS or IIS Express.</span></span>

<span data-ttu-id="2821f-171">Visual Studio에서 기본 실행 프로필은 IIS Express용입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-171">In Visual Studio, the default launch profile is for IIS Express.</span></span> <span data-ttu-id="2821f-172">프로젝트를 콘솔 응용 프로그램으로 실행하려면 다음 스크린샷에 표시된 것처럼 선택한 프로필을 수동으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-172">To run the project as a console application, manually change the selected profile, as shown in the following screen shot.</span></span>

![콘솔 앱 프로필 선택](httpsys/_static/vs-choose-profile.png)

## <a name="preregister-url-prefixes-and-configure-ssl"></a><span data-ttu-id="2821f-174">URL 접두사 미리 등록 및 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-174">Preregister URL prefixes and configure SSL</span></span>

<span data-ttu-id="2821f-175">IIS와 HTTP.sys는 모두 기본 Http.Sys 커널 모드 드라이버를 사용하여 요청을 수신하고 초기 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-175">Both IIS and HTTP.sys rely on the underlying Http.Sys kernel mode driver to listen for requests and do initial processing.</span></span> <span data-ttu-id="2821f-176">IIS에서 관리 UI는 모든 항목을 구성하는 상대적으로 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-176">In IIS, the management UI gives you a relatively easy way to configure everything.</span></span> <span data-ttu-id="2821f-177">그러나 Http.Sys는 직접 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-177">However, you need to configure Http.Sys yourself.</span></span> <span data-ttu-id="2821f-178">작업 수행을 위한 기본 도구는 *netsh.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-178">The built-in tool for doing that's *netsh.exe*.</span></span> 

<span data-ttu-id="2821f-179">*netsh.exe*를 사용하면 URL 접두사를 예약하고 SSL 인증서를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-179">With *netsh.exe* you can reserve URL prefixes and assign SSL certificates.</span></span> <span data-ttu-id="2821f-180">도구를 사용하려면 관리 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-180">The tool requires administrative privileges.</span></span>

<span data-ttu-id="2821f-181">다음 예제에서는 포트 80 및 443에 대해 URL 접두사를 예약하는 데 필요한 최소한의 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-181">The following example shows the minimum needed to reserve URL prefixes for ports 80 and 443:</span></span>

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

<span data-ttu-id="2821f-182">다음 예제에서는 SSL 인증서를 할당하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-182">The following example shows how to assign an SSL certificate:</span></span>

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
```

<span data-ttu-id="2821f-183">다음은 *netsh.exe*에 대한 참조 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-183">Here is the reference documentation for *netsh.exe*:</span></span>

* [<span data-ttu-id="2821f-184">HTTP(Hypertext Transfer Protocol)에 대한 Netsh 명령</span><span class="sxs-lookup"><span data-stu-id="2821f-184">Netsh Commands for Hypertext Transfer Protocol (HTTP)</span></span>](https://technet.microsoft.com/library/cc725882.aspx)
* [<span data-ttu-id="2821f-185">UrlPrefix 문자열</span><span class="sxs-lookup"><span data-stu-id="2821f-185">UrlPrefix Strings</span></span>](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

<span data-ttu-id="2821f-186">다음 리소스는 여러 시나리오에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-186">The following resources provide detailed instructions for several scenarios.</span></span> <span data-ttu-id="2821f-187">HttpListener를 참조하는 문서는 모두 Http.Sys를 기반으로 하므로 HTTP.sys에 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-187">Articles that refer to HttpListener apply equally to HTTP.sys, as both are based on Http.Sys.</span></span>

* [<span data-ttu-id="2821f-188">방법: SSL 인증서로 포트 구성</span><span class="sxs-lookup"><span data-stu-id="2821f-188">How to: Configure a Port with an SSL Certificate</span></span>](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* <span data-ttu-id="2821f-189">[HTTPS 통신 - HttpListener 기반 호스팅 및 클라이언트 인증](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) 이는 타사 블로그이며 비교적 오래됐지만 여전히 유용한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-189">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) This is a third-party blog and is fairly old but still has useful information.</span></span>
* <span data-ttu-id="2821f-190">[방법: SSL 단순 서버로 HttpListener 또는 Http 서버 비관리 코드(C++)를 사용한 연습](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) 유용한 정보가 있는 오래된 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-190">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) This too is an older blog with useful information.</span></span>

<span data-ttu-id="2821f-191">다음은 *netsh.exe* 명령줄보다 쉽게 사용할 수 있는 몇 가지 타사 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-191">Here are some third-party tools that can be easier to use than the *netsh.exe* command line.</span></span> <span data-ttu-id="2821f-192">이러한 도구는 Microsoft에서 제공되거나 보증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-192">These are not provided by or endorsed by Microsoft.</span></span> <span data-ttu-id="2821f-193">*netsh.exe* 자체는 관리자 권한이 필요하므로 도구는 기본적으로 관리자 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-193">The tools run as administrator by default, since *netsh.exe* itself requires administrator privileges.</span></span>

* <span data-ttu-id="2821f-194">[http.sys 관리자](http://httpsysmanager.codeplex.com/)는 SSL 인증서 및 옵션, 접두사 예약 및 인증서 신뢰 목록의 나열 및 구성을 위한 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-194">[http.sys Manager](http://httpsysmanager.codeplex.com/) provides UI for listing and configuring SSL certificates and options, prefix reservations, and certificate trust lists.</span></span> 
* <span data-ttu-id="2821f-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx)를 통해 SSL 인증서와 URL 접두사를 나열하거나 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) lets you list or configure SSL certificates and URL prefixes.</span></span> <span data-ttu-id="2821f-196">UI는 http.sys 관리자보다 성능이 우수하며 몇 가지 추가 구성 옵션을 노출하지만 그렇지 않은 경우 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-196">The UI is more refined than http.sys Manager and exposes a few more configuration options, but otherwise it provides similar functionality.</span></span> <span data-ttu-id="2821f-197">새 CTL(인증서 신뢰 목록)을 만들 수 없지만 기존 것을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2821f-197">It cannot create a new certificate trust list (CTL), but can assign existing ones.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

## <a name="next-steps"></a><span data-ttu-id="2821f-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2821f-198">Next steps</span></span>

<span data-ttu-id="2821f-199">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2821f-199">For more information, see the following resources:</span></span>

* [<span data-ttu-id="2821f-200">이 문서에 대한 샘플 앱</span><span class="sxs-lookup"><span data-stu-id="2821f-200">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)
* [<span data-ttu-id="2821f-201">HTTP.sys 소스 코드</span><span class="sxs-lookup"><span data-stu-id="2821f-201">HTTP.sys source code</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="2821f-202">호스팅</span><span class="sxs-lookup"><span data-stu-id="2821f-202">Hosting</span></span>](xref:fundamentals/hosting)
