---
title: ASP.NET Core에서 HTTP.sys 웹 서버 구현
author: guardrex
description: Windows의 ASP.NET Core에 대한 웹 서버인 HTTP.sys에 대해 알아봅니다. HTTP.sys 커널 모드 드라이버를 기반으로 한 HTTP.sys는 IIS 없이 인터넷에 대한 직접 연결에 사용될 수 있는 Kestrel에 대한 대안입니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/01/2018
uid: fundamentals/servers/httpsys
ms.openlocfilehash: 8810fd295e8c4269812e712ce2fdc9b9fa2bbb4f
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861695"
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="6eb32-104">ASP.NET Core에서 HTTP.sys 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="6eb32-104">HTTP.sys web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="6eb32-105">작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6eb32-105">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Luke Latham](https://github.com/guardrex)</span></span>

> [!NOTE]
> <span data-ttu-id="6eb32-106">이 주제는 ASP.NET Core 2.0 이상에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-106">This topic applies to ASP.NET Core 2.0 or later.</span></span> <span data-ttu-id="6eb32-107">이전 버전의 ASP.NET Core에서 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-107">In earlier versions of ASP.NET Core, HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener).</span></span>

<span data-ttu-id="6eb32-108">[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys)는 Windows에서만 실행되는 [ASP.NET Core에 대한 웹 서버](xref:fundamentals/servers/index)입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-108">[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) is a [web server for ASP.NET Core](xref:fundamentals/servers/index) that only runs on Windows.</span></span> <span data-ttu-id="6eb32-109">HTTP.sys는 [Kestrel](xref:fundamentals/servers/kestrel) 서버에 대한 대안이며 Kestel이 제공하지 않는 일부 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-109">HTTP.sys is an alternative to [Kestrel](xref:fundamentals/servers/kestrel) server and offers some features that Kestrel doesn't provide.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6eb32-110">HTTP.sys는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)과 호환되지 않으므로 IIS 또는 IIS Express와 함께 사용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-110">HTTP.sys is incompatible with the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and can't be used with IIS or IIS Express.</span></span>

<span data-ttu-id="6eb32-111">HTTP.sys는 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-111">HTTP.sys supports the following features:</span></span>

* [<span data-ttu-id="6eb32-112">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="6eb32-112">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
* <span data-ttu-id="6eb32-113">포트 공유</span><span class="sxs-lookup"><span data-stu-id="6eb32-113">Port sharing</span></span>
* <span data-ttu-id="6eb32-114">SNI를 사용하는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6eb32-114">HTTPS with SNI</span></span>
* <span data-ttu-id="6eb32-115">TLS를 통한 HTTP/2(Windows 10 이상)</span><span class="sxs-lookup"><span data-stu-id="6eb32-115">HTTP/2 over TLS (Windows 10 or later)</span></span>
* <span data-ttu-id="6eb32-116">직접 파일 전송</span><span class="sxs-lookup"><span data-stu-id="6eb32-116">Direct file transmission</span></span>
* <span data-ttu-id="6eb32-117">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="6eb32-117">Response caching</span></span>
* <span data-ttu-id="6eb32-118">WebSockets(Windows 8 이상)</span><span class="sxs-lookup"><span data-stu-id="6eb32-118">WebSockets (Windows 8 or later)</span></span>

<span data-ttu-id="6eb32-119">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="6eb32-119">Supported Windows versions:</span></span>

* <span data-ttu-id="6eb32-120">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="6eb32-120">Windows 7 or later</span></span>
* <span data-ttu-id="6eb32-121">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="6eb32-121">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="6eb32-122">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6eb32-122">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-httpsys"></a><span data-ttu-id="6eb32-123">HTTP.sys를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="6eb32-123">When to use HTTP.sys</span></span>

<span data-ttu-id="6eb32-124">HTTP.sys는 다음과 같은 배포에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-124">HTTP.sys is useful for deployments where:</span></span>

* <span data-ttu-id="6eb32-125">IIS를 사용하지 않고 인터넷에 서버를 직접 노출해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="6eb32-125">There's a need to expose the server directly to the Internet without using IIS.</span></span>

  ![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

* <span data-ttu-id="6eb32-127">내부 배포에는 [Windows 인증](xref:security/authentication/windowsauth)처럼 Kestrel에서 사용할 수 없는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-127">An internal deployment requires a feature not available in Kestrel, such as [Windows Authentication](xref:security/authentication/windowsauth).</span></span>

  ![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

<span data-ttu-id="6eb32-129">HTTP.sys는 많은 유형의 공격으로부터 보호하고 모든 기능을 갖춘 웹 서버의 견고성, 보안 및 확장성을 제공하는 완성도 높은 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-129">HTTP.sys is mature technology that protects against many types of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="6eb32-130">IIS 자체는 HTTP.sys 위에 HTTP 수신기로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-130">IIS itself runs as an HTTP listener on top of HTTP.sys.</span></span>

## <a name="http2-support"></a><span data-ttu-id="6eb32-131">HTTP/2 지원</span><span class="sxs-lookup"><span data-stu-id="6eb32-131">HTTP/2 support</span></span>

<span data-ttu-id="6eb32-132">다음 기본 요구 사항이 충족되는 경우 ASP.NET Core 앱에 대해[HTTP/2](https://httpwg.org/specs/rfc7540.html)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-132">[HTTP/2](https://httpwg.org/specs/rfc7540.html) is enabled for ASP.NET Core apps if the following base requirements are met:</span></span>

* <span data-ttu-id="6eb32-133">Windows Server 2016/Windows 10 이상</span><span class="sxs-lookup"><span data-stu-id="6eb32-133">Windows Server 2016/Windows 10 or later</span></span>
* <span data-ttu-id="6eb32-134">[ALPN(Application-Layer Protocol Negotiation)](https://tools.ietf.org/html/rfc7301#section-3) 연결</span><span class="sxs-lookup"><span data-stu-id="6eb32-134">[Application-Layer Protocol Negotiation (ALPN)](https://tools.ietf.org/html/rfc7301#section-3) connection</span></span>
* <span data-ttu-id="6eb32-135">TLS 1.2 이상 연결</span><span class="sxs-lookup"><span data-stu-id="6eb32-135">TLS 1.2 or later connection</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="6eb32-136">HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/2`를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-136">If an HTTP/2 connection is established, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) reports `HTTP/2`.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="6eb32-137">HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/1.1`을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-137">If an HTTP/2 connection is established, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) reports `HTTP/1.1`.</span></span>

::: moniker-end

<span data-ttu-id="6eb32-138">HTTP/2는 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-138">HTTP/2 is enabled by default.</span></span> <span data-ttu-id="6eb32-139">HTTP/2 연결이 설정되지 않는 경우 연결이 HTTP/1.1로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-139">If an HTTP/2 connection isn't established, the connection falls back to HTTP/1.1.</span></span> <span data-ttu-id="6eb32-140">Windows의 이후 릴리스에서는 HTTP.sys를 사용하여 HTTP/2를 사용하지 않도록 하는 기능을 포함하여 HTTP/2 구성 플래그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-140">In a future release of Windows, HTTP/2 configuration flags will be available, including the ability to disable HTTP/2 with HTTP.sys.</span></span>

## <a name="kernel-mode-authentication-with-kerberos"></a><span data-ttu-id="6eb32-141">Kerberos를 사용하여 커널 모드 인증</span><span class="sxs-lookup"><span data-stu-id="6eb32-141">Kernel mode authentication with Kerberos</span></span>

<span data-ttu-id="6eb32-142">HTTP.sys는 Kerberos 인증 프로토콜을 사용하여 커널 모드 인증에 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-142">HTTP.sys delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="6eb32-143">사용자 모드 인증은 Kerberos 및 HTTP.sys로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-143">User mode authentication isn't supported with Kerberos and HTTP.sys.</span></span> <span data-ttu-id="6eb32-144">머신 계정은 Active Directory에서 가져온 Kerberos 토큰/티켓의 암호를 해독하는 데 사용되고 사용자를 인증하는 서버에 클라이언트에 의해 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-144">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="6eb32-145">앱의 사용자가 아닌 호스트에 대해 SPN(서비스 사용자 이름)을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-145">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

## <a name="how-to-use-httpsys"></a><span data-ttu-id="6eb32-146">HTTP.sys 사용 방법</span><span class="sxs-lookup"><span data-stu-id="6eb32-146">How to use HTTP.sys</span></span>

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a><span data-ttu-id="6eb32-147">HTTP.sys를 사용하도록 ASP.NET Core 앱 구성</span><span class="sxs-lookup"><span data-stu-id="6eb32-147">Configure the ASP.NET Core app to use HTTP.sys</span></span>

1. <span data-ttu-id="6eb32-148">[Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.App/))(ASP.NET Core 2.1이상)를 사용할 경우 프로젝트 파일의 패키지 참조가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-148">A package reference in the project file isn't required when using the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)) (ASP.NET Core 2.1 or later).</span></span> <span data-ttu-id="6eb32-149">`Microsoft.AspNetCore.App` 메타패키지를 사용하지 않는 경우 [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-149">When not using the `Microsoft.AspNetCore.App` metapackage, add a package reference to [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/).</span></span>

2. <span data-ttu-id="6eb32-150">웹 호스트를 빌드할 때 [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) 확장 메서드를 호출하여 필요한 [HTTP.sys 옵션](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-150">Call the [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) extension method when building the web host, specifying any required [HTTP.sys options](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions):</span></span>

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   <span data-ttu-id="6eb32-151">추가 HTTP.sys 구성은 [레지스트리 설정](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows)을 통해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-151">Additional HTTP.sys configuration is handled through [registry settings](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows).</span></span>

   <span data-ttu-id="6eb32-152">**HTTP.sys 옵션**</span><span class="sxs-lookup"><span data-stu-id="6eb32-152">**HTTP.sys options**</span></span>

   | <span data-ttu-id="6eb32-153">속성</span><span class="sxs-lookup"><span data-stu-id="6eb32-153">Property</span></span> | <span data-ttu-id="6eb32-154">설명</span><span class="sxs-lookup"><span data-stu-id="6eb32-154">Description</span></span> | <span data-ttu-id="6eb32-155">기본</span><span class="sxs-lookup"><span data-stu-id="6eb32-155">Default</span></span> |
   | -------- | ----------- | :-----: |
   | [<span data-ttu-id="6eb32-156">AllowSynchronousIO</span><span class="sxs-lookup"><span data-stu-id="6eb32-156">AllowSynchronousIO</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.allowsynchronousio) | <span data-ttu-id="6eb32-157">`HttpContext.Request.Body` 및 `HttpContext.Response.Body`에 대해 동기 입력/출력이 허용되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-157">Control whether synchronous input/output is allowed for the `HttpContext.Request.Body` and `HttpContext.Response.Body`.</span></span> | `true` |
   | [<span data-ttu-id="6eb32-158">Authentication.AllowAnonymous</span><span class="sxs-lookup"><span data-stu-id="6eb32-158">Authentication.AllowAnonymous</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.allowanonymous) | <span data-ttu-id="6eb32-159">익명 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-159">Allow anonymous requests.</span></span> | `true` |
   | [<span data-ttu-id="6eb32-160">Authentication.Schemes</span><span class="sxs-lookup"><span data-stu-id="6eb32-160">Authentication.Schemes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.schemes) | <span data-ttu-id="6eb32-161">허용되는 인증 체계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-161">Specify the allowed authentication schemes.</span></span> <span data-ttu-id="6eb32-162">수신기를 삭제하기 전에 언제든지 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-162">May be modified at any time prior to disposing the listener.</span></span> <span data-ttu-id="6eb32-163">값은 [AuthenticationSchemes 열거형](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes): `Basic`, `Kerberos`, `Negotiate`, `None`, `NTLM`에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-163">Values are provided by the [AuthenticationSchemes enum](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes): `Basic`, `Kerberos`, `Negotiate`, `None`, and `NTLM`.</span></span> | `None` |
   | [<span data-ttu-id="6eb32-164">EnableResponseCaching</span><span class="sxs-lookup"><span data-stu-id="6eb32-164">EnableResponseCaching</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.enableresponsecaching) | <span data-ttu-id="6eb32-165">적합한 헤더가 있는 응답에 대해 [커널 모드](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) 캐싱을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-165">Attempt [kernel-mode](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) caching for responses with eligible headers.</span></span> <span data-ttu-id="6eb32-166">응답에 `Set-Cookie`, `Vary` 또는 `Pragma` 헤더가 포함될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-166">The response may not include `Set-Cookie`, `Vary`, or `Pragma` headers.</span></span> <span data-ttu-id="6eb32-167">`public` 및 `shared-max-age` 또는 `max-age` 값인 `Cache-Control` 헤더나 `Expires` 헤더가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-167">It must include a `Cache-Control` header that's `public` and either a `shared-max-age` or `max-age` value, or an `Expires` header.</span></span> | `true` |
   | [<span data-ttu-id="6eb32-168">MaxAccepts</span><span class="sxs-lookup"><span data-stu-id="6eb32-168">MaxAccepts</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxaccepts) | <span data-ttu-id="6eb32-169">최대 동시 승인 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-169">The maximum number of concurrent accepts.</span></span> | <span data-ttu-id="6eb32-170">5 &times; [Environment.<br>ProcessorCount](/dotnet/api/system.environment.processorcount)</span><span class="sxs-lookup"><span data-stu-id="6eb32-170">5 &times; [Environment.<br>ProcessorCount](/dotnet/api/system.environment.processorcount)</span></span> |
   | [<span data-ttu-id="6eb32-171">MaxConnections</span><span class="sxs-lookup"><span data-stu-id="6eb32-171">MaxConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxconnections) | <span data-ttu-id="6eb32-172">허용되는 최대 동시 연결 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-172">The maximum number of concurrent connections to accept.</span></span> <span data-ttu-id="6eb32-173">무한의 경우 `-1`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-173">Use `-1` for infinite.</span></span> <span data-ttu-id="6eb32-174">레지스트리의 시스템 수준 설정을 사용하려면 `null`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-174">Use `null` to use the registry's machine-wide setting.</span></span> | `null`<br><span data-ttu-id="6eb32-175">(제한 없음)</span><span class="sxs-lookup"><span data-stu-id="6eb32-175">(unlimited)</span></span> |
   | [<span data-ttu-id="6eb32-176">MaxRequestBodySize</span><span class="sxs-lookup"><span data-stu-id="6eb32-176">MaxRequestBodySize</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) | <span data-ttu-id="6eb32-177"><a href="#maxrequestbodysize">MaxRequestBodySize</a> 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb32-177">See the <a href="#maxrequestbodysize">MaxRequestBodySize</a> section.</span></span> | <span data-ttu-id="6eb32-178">30000000바이트</span><span class="sxs-lookup"><span data-stu-id="6eb32-178">30000000 bytes</span></span><br><span data-ttu-id="6eb32-179">(~28.6MB)</span><span class="sxs-lookup"><span data-stu-id="6eb32-179">(~28.6 MB)</span></span> |
   | [<span data-ttu-id="6eb32-180">RequestQueueLimit</span><span class="sxs-lookup"><span data-stu-id="6eb32-180">RequestQueueLimit</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.requestqueuelimit) | <span data-ttu-id="6eb32-181">큐에 대기할 수 있는 최대 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-181">The maximum number of requests that can be queued.</span></span> | <span data-ttu-id="6eb32-182">1000</span><span class="sxs-lookup"><span data-stu-id="6eb32-182">1000</span></span> |
   | [<span data-ttu-id="6eb32-183">ThrowWriteExceptions</span><span class="sxs-lookup"><span data-stu-id="6eb32-183">ThrowWriteExceptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.throwwriteexceptions) | <span data-ttu-id="6eb32-184">클라이언트 연결 해제로 인해 실패한 응답 본문 쓰기가 예외를 throw하거나 정상적으로 완료되어야 하는지 여부를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-184">Indicate if response body writes that fail due to client disconnects should throw exceptions or complete normally.</span></span> | `false`<br><span data-ttu-id="6eb32-185">(정상적으로 완료)</span><span class="sxs-lookup"><span data-stu-id="6eb32-185">(complete normally)</span></span> |
   | [<span data-ttu-id="6eb32-186">Timeouts</span><span class="sxs-lookup"><span data-stu-id="6eb32-186">Timeouts</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts) | <span data-ttu-id="6eb32-187">레지스트리에 구성될 수도 있는 HTTP.sys [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) 구성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-187">Expose the HTTP.sys [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) configuration, which may also be configured in the registry.</span></span> <span data-ttu-id="6eb32-188">API 링크를 따라 기본값을 포함하여 각 설정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="6eb32-188">Follow the API links to learn more about each setting, including default values:</span></span><ul><li><span data-ttu-id="6eb32-189">[TimeoutManager.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.drainentitybody) &ndash; HTTP 서버 API가 지속적 연결에서 엔터티 본문을 비우는 데 허용되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-189">[TimeoutManager.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.drainentitybody) &ndash; Time allowed for the HTTP Server API to drain the entity body on a Keep-Alive connection.</span></span></li><li><span data-ttu-id="6eb32-190">[TimeoutManager.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.entitybody) &ndash; 요청 엔터티가 도착하는 데 허용되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-190">[TimeoutManager.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.entitybody) &ndash; Time allowed for the request entity body to arrive.</span></span></li><li><span data-ttu-id="6eb32-191">[TimeoutManager.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.headerwait) &ndash; HTTP 서버 API가 요청 헤더를 구문 분석하는 데 허용되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-191">[TimeoutManager.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.headerwait) &ndash; Time allowed for the HTTP Server API to parse the request header.</span></span></li><li><span data-ttu-id="6eb32-192">[TimeoutManager.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.idleconnection) &ndash; 유휴 연결에 허용되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-192">[TimeoutManager.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.idleconnection) &ndash; Time allowed for an idle connection.</span></span></li><li><span data-ttu-id="6eb32-193">[TimeoutManager.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.minsendbytespersecond) &ndash; 응답에 대한 최소 전송 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-193">[TimeoutManager.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.minsendbytespersecond) &ndash; The minimum send rate for the response.</span></span></li><li><span data-ttu-id="6eb32-194">[TimeoutManager.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.requestqueue) &ndash; 앱이 선택하기 전에 요청이 요청 큐에 남아 있는 데 허용되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-194">[TimeoutManager.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager.requestqueue) &ndash; Time allowed for the request to remain in the request queue before the app picks it up.</span></span></li></ul> |  |
   | [<span data-ttu-id="6eb32-195">UrlPrefixes</span><span class="sxs-lookup"><span data-stu-id="6eb32-195">UrlPrefixes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes) | <span data-ttu-id="6eb32-196">[UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection)을 지정하여 HTTP.sys를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-196">Specify the [UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection) to register with HTTP.sys.</span></span> <span data-ttu-id="6eb32-197">컬렉션에 접두사를 추가하는 데 사용되는 [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add)가 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-197">The most useful is [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add), which is used to add a prefix to the collection.</span></span> <span data-ttu-id="6eb32-198">이러한 API는 수신기를 삭제하기 전에 언제든지 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-198">These may be modified at any time prior to disposing the listener.</span></span> |  |

   <a name="maxrequestbodysize"></a>
   <span data-ttu-id="6eb32-199">**MaxRequestBodySize**</span><span class="sxs-lookup"><span data-stu-id="6eb32-199">**MaxRequestBodySize**</span></span>

   <span data-ttu-id="6eb32-200">요청 본문에 대해 허용되는 최대 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-200">The maximum allowed size of any request body in bytes.</span></span> <span data-ttu-id="6eb32-201">`null`로 설정하면 최대 요청 본문 크기는 무제한입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-201">When set to `null`, the maximum request body size is unlimited.</span></span> <span data-ttu-id="6eb32-202">항상 무제한인 업그레이드된 연결에는 이 제한이 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-202">This limit has no effect on upgraded connections, which are always unlimited.</span></span>

   <span data-ttu-id="6eb32-203">단일 `IActionResult`에 대해 ASP.NET Core MVC 앱에서 제한을 재정의할 때는 작업 메서드에서 [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 특성을 사용하는 방법이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-203">The recommended method to override the limit in an ASP.NET Core MVC app for a single `IActionResult` is to use the [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) attribute on an action method:</span></span>

   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   <span data-ttu-id="6eb32-204">앱에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-204">An exception is thrown if the app attempts to configure the limit on a request after the app has started reading the request.</span></span> <span data-ttu-id="6eb32-205">`IsReadOnly` 속성을 사용하여 `MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-205">An `IsReadOnly` property can be used to indicate if the `MaxRequestBodySize` property is in a read-only state, meaning it's too late to configure the limit.</span></span>

   <span data-ttu-id="6eb32-206">앱에서 요청별로 [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize)를 재정의해야 하는 경우 [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-206">If the app should override [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) per-request, use the [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature):</span></span>

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

3. <span data-ttu-id="6eb32-207">Visual Studio를 사용하는 경우 앱이 IIS 또는 IIS Express를 실행하도록 구성되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-207">If using Visual Studio, make sure the app isn't configured to run IIS or IIS Express.</span></span>

   <span data-ttu-id="6eb32-208">Visual Studio에서 기본 실행 프로필은 IIS Express용입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-208">In Visual Studio, the default launch profile is for IIS Express.</span></span> <span data-ttu-id="6eb32-209">프로젝트를 콘솔 앱으로 실행하려면 다음 스크린샷에 표시된 것처럼 선택한 프로필을 수동으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-209">To run the project as a console app, manually change the selected profile, as shown in the following screen shot:</span></span>

   ![콘솔 앱 프로필 선택](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a><span data-ttu-id="6eb32-211">Windows Server 구성</span><span class="sxs-lookup"><span data-stu-id="6eb32-211">Configure Windows Server</span></span>

1. <span data-ttu-id="6eb32-212">앱이 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우 .NET Core, .NET Framework 또는 둘 다(앱이 NET Framework를 대상으로 하는 .NET Core 앱인 경우)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-212">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd), install .NET Core, .NET Framework, or both (if the app is a .NET Core app targeting the .NET Framework).</span></span>

   * <span data-ttu-id="6eb32-213">**.NET Core** &ndash; 앱에 .NET Core가 필요한 경우 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 .NET Core 설치 관리자를 가져와 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-213">**.NET Core** &ndash; If the app requires .NET Core, obtain and run the .NET Core installer from [.NET All Downloads](https://www.microsoft.com/net/download/all).</span></span>
   * <span data-ttu-id="6eb32-214">**.NET Framework** &ndash; 앱에 .NET Framework가 필요한 경우 [.NET Framework: 설치 가이드](/dotnet/framework/install/)를 참조하여 설치 지침을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-214">**.NET Framework** &ndash; If the app requires .NET Framework, see [.NET Framework: Installation guide](/dotnet/framework/install/) to find installation instructions.</span></span> <span data-ttu-id="6eb32-215">필수 .NET Framework를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-215">Install the required .NET Framework.</span></span> <span data-ttu-id="6eb32-216">최신 .NET Framework의 설치 관리자는 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-216">The installer for the latest .NET Framework can be found at [.NET All Downloads](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="6eb32-217">앱에 대한 URL 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-217">Configure URLs and ports for the app.</span></span>

   <span data-ttu-id="6eb32-218">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-218">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="6eb32-219">URL 접두사 및 포트를 구성하려면 다음을 사용하는 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-219">To configure URL prefixes and ports, options include using:</span></span>

   * [<span data-ttu-id="6eb32-220">UseUrls</span><span class="sxs-lookup"><span data-stu-id="6eb32-220">UseUrls</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
   * <span data-ttu-id="6eb32-221">`urls` 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="6eb32-221">`urls` command-line argument</span></span>
   * <span data-ttu-id="6eb32-222">`ASPNETCORE_URLS`환경 변수</span><span class="sxs-lookup"><span data-stu-id="6eb32-222">`ASPNETCORE_URLS` environment variable</span></span>
   * [<span data-ttu-id="6eb32-223">UrlPrefixes</span><span class="sxs-lookup"><span data-stu-id="6eb32-223">UrlPrefixes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)

   <span data-ttu-id="6eb32-224">다음 코드 예제에서는 [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-224">The following code example shows how to use [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes):</span></span>

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=11)]

   <span data-ttu-id="6eb32-225">`UrlPrefixes`의 장점은 형식이 잘못된 접두사에 대해 오류 메시지가 즉시 생성된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-225">An advantage of `UrlPrefixes` is that an error message is generated immediately for improperly formatted prefixes.</span></span>

   <span data-ttu-id="6eb32-226">`UrlPrefixes`의 설정은 `UseUrls`/`urls`/`ASPNETCORE_URLS` 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-226">The settings in `UrlPrefixes` override `UseUrls`/`urls`/`ASPNETCORE_URLS` settings.</span></span> <span data-ttu-id="6eb32-227">따라서 `UseUrls`, `urls` 및 `ASPNETCORE_URLS` 환경 변수의 장점은 Kestrel과 HTTP.sys 간을 쉽게 전환할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-227">Therefore, an advantage of `UseUrls`, `urls`, and the `ASPNETCORE_URLS` environment variable is that it's easier to switch between Kestrel and HTTP.sys.</span></span> <span data-ttu-id="6eb32-228">`UseUrls`, `urls` 및 `ASPNETCORE_URLS`에 대한 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb32-228">For more information on `UseUrls`, `urls`, and `ASPNETCORE_URLS`, see the [Host in ASP.NET Core](xref:fundamentals/host/index) topic.</span></span>

   <span data-ttu-id="6eb32-229">HTTP.sys는 [HTTP Server API UrlPrefix 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-229">HTTP.sys uses the [HTTP Server API UrlPrefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span>

   > [!WARNING]
   > <span data-ttu-id="6eb32-230">최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-230">Top-level wildcard bindings (`http://*:80/` and `http://+:80`) should **not** be used.</span></span> <span data-ttu-id="6eb32-231">최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-231">Top-level wildcard bindings can open up your app to security vulnerabilities.</span></span> <span data-ttu-id="6eb32-232">강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-232">This applies to both strong and weak wildcards.</span></span> <span data-ttu-id="6eb32-233">와일드카드보다는 명시적 호스트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-233">Use explicit host names rather than wildcards.</span></span> <span data-ttu-id="6eb32-234">전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임).</span><span class="sxs-lookup"><span data-stu-id="6eb32-234">Subdomain wildcard binding (for example, `*.mysub.com`) doesn't have this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="6eb32-235">자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb32-235">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

3. <span data-ttu-id="6eb32-236">URL 접두사를 미리 등록하여 HTTP.sys에 대해 바인딩하고 x.509 인증서를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-236">Preregister URL prefixes to bind to HTTP.sys and set up x.509 certificates.</span></span>

   <span data-ttu-id="6eb32-237">URL 접두사가 Windows에 미리 등록되어 있지 않은 경우 관리자 권한으로 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-237">If URL prefixes aren't preregistered in Windows, run the app with administrator privileges.</span></span> <span data-ttu-id="6eb32-238">1024보다 큰 포트 번호로 HTTP(HTTPS 아님)를 사용하여 localhost에 바인딩하는 경우에만</span><span class="sxs-lookup"><span data-stu-id="6eb32-238">The only exception is when binding to localhost using HTTP (not HTTPS) with a port number greater than 1024.</span></span> <span data-ttu-id="6eb32-239">관리자 권한이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-239">In that case, administrator privileges aren't required.</span></span>

   1. <span data-ttu-id="6eb32-240">HTTP.sys 구성에 대한 기본 제공 도구는 *netsh.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-240">The built-in tool for configuring HTTP.sys is *netsh.exe*.</span></span> <span data-ttu-id="6eb32-241">*netsh.exe*는 URL 접두사를 예약하고 X.509 인증서를 할당하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-241">*netsh.exe* is used to reserve URL prefixes and assign X.509 certificates.</span></span> <span data-ttu-id="6eb32-242">도구를 사용하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-242">The tool requires administrator privileges.</span></span>

      <span data-ttu-id="6eb32-243">다음 예제에서는 포트 80 및 443에 대해 URL 접두사를 예약하는 명령을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-243">The following example shows the commands to reserve URL prefixes for ports 80 and 443:</span></span>

      ```console
      netsh http add urlacl url=http://+:80/ user=Users
      netsh http add urlacl url=https://+:443/ user=Users
      ```

      <span data-ttu-id="6eb32-244">다음 예제에서는 X.509 인증서를 할당하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-244">The following example shows how to assign an X.509 certificate:</span></span>

      ```console
      netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid="{00000000-0000-0000-0000-000000000000}"
      ```

      <span data-ttu-id="6eb32-245">*netsh.exe*에 대한 참조 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-245">Reference documentation for *netsh.exe*:</span></span>

      * [<span data-ttu-id="6eb32-246">HTTP(Hypertext Transfer Protocol)에 대한 Netsh 명령</span><span class="sxs-lookup"><span data-stu-id="6eb32-246">Netsh Commands for Hypertext Transfer Protocol (HTTP)</span></span>](https://technet.microsoft.com/library/cc725882.aspx)
      * [<span data-ttu-id="6eb32-247">UrlPrefix 문자열</span><span class="sxs-lookup"><span data-stu-id="6eb32-247">UrlPrefix Strings</span></span>](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

   2. <span data-ttu-id="6eb32-248">필요한 경우, 자체 서명 X.509 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-248">Create self-signed X.509 certificates, if required.</span></span>

      [!INCLUDE [How to make an X.509 cert](../../includes/make-x509-cert.md)]

4. <span data-ttu-id="6eb32-249">방화벽 포트를 열어 HTTP.sys에 도달하는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-249">Open firewall ports to allow traffic to reach HTTP.sys.</span></span> <span data-ttu-id="6eb32-250">*netsh.exe* 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-250">Use *netsh.exe* or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="6eb32-251">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="6eb32-251">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="6eb32-252">인터넷 또는 회사 네트워크의 요청과 상호 작용하는 HTTP.sys에서 호스팅하는 앱의 경우, 프록시 서버 및 부하 분산 장치 뒤에서 호스팅할 때 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eb32-252">For apps hosted by HTTP.sys that interact with requests from the Internet or a corporate network, additional configuration might be required when hosting behind proxy servers and load balancers.</span></span> <span data-ttu-id="6eb32-253">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eb32-253">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6eb32-254">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6eb32-254">Additional resources</span></span>

* <span data-ttu-id="6eb32-255">[HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)(HTTP 서버 API)</span><span class="sxs-lookup"><span data-stu-id="6eb32-255">[HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)</span></span>
* [<span data-ttu-id="6eb32-256">aspnet/HttpSysServer GitHub 리포지토리(소스 코드)</span><span class="sxs-lookup"><span data-stu-id="6eb32-256">aspnet/HttpSysServer GitHub repository (source code)</span></span>](https://github.com/aspnet/HttpSysServer/)
* <xref:fundamentals/host/index>
* <xref:test/troubleshoot>
