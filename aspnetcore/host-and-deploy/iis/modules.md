---
title: "IIS 모듈을 사용 하 여 ASP.NET 코어"
author: guardrex
description: "ASP.NET Core 응용 프로그램에 대 한 활성 및 비활성 IIS 모듈을 설명 하는 문서를 참조 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/08/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/modules
ms.openlocfilehash: b7c81f2851a932cd12553af4a2655eb9f1f7bc64
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="using-iis-modules-with-aspnet-core"></a><span data-ttu-id="62038-103">IIS 모듈을 사용 하 여 ASP.NET 코어</span><span class="sxs-lookup"><span data-stu-id="62038-103">Using IIS Modules with ASP.NET Core</span></span>

<span data-ttu-id="62038-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="62038-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="62038-105">ASP.NET Core 응용 프로그램의 역방향 프록시 구성에서 IIS에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62038-105">ASP.NET Core applications are hosted by IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="62038-106">네이티브 IIS 모듈의 일부와 모든 관리 되는 IIS 모듈 ASP.NET Core 응용 프로그램에 대 한 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62038-106">Some of the native IIS modules and all of the IIS managed modules aren't available to process requests for ASP.NET Core apps.</span></span> <span data-ttu-id="62038-107">대부분의 경우 ASP.NET Core IIS 네이티브 및 관리 되는 모듈의 기능에 대 한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-107">In many cases, ASP.NET Core offers an alternative to the features of IIS native and managed modules.</span></span>

## <a name="native-modules"></a><span data-ttu-id="62038-108">네이티브 모듈</span><span class="sxs-lookup"><span data-stu-id="62038-108">Native Modules</span></span>

<span data-ttu-id="62038-109">Module</span><span class="sxs-lookup"><span data-stu-id="62038-109">Module</span></span> | <span data-ttu-id="62038-110">.NET Core Active</span><span class="sxs-lookup"><span data-stu-id="62038-110">.NET Core Active</span></span> | <span data-ttu-id="62038-111">ASP.NET Core 옵션</span><span class="sxs-lookup"><span data-stu-id="62038-111">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="62038-112">**익명 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-112">**Anonymous Authentication**</span></span><br>`AnonymousAuthenticationModule` | <span data-ttu-id="62038-113">예</span><span class="sxs-lookup"><span data-stu-id="62038-113">Yes</span></span> | 
<span data-ttu-id="62038-114">**기본 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-114">**Basic Authentication**</span></span><br>`BasicAuthenticationModule` | <span data-ttu-id="62038-115">예</span><span class="sxs-lookup"><span data-stu-id="62038-115">Yes</span></span> | 
<span data-ttu-id="62038-116">**클라이언트 인증 매핑 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-116">**Client Certification Mapping Authentication**</span></span><br>`CertificateMappingAuthenticationModule` | <span data-ttu-id="62038-117">예</span><span class="sxs-lookup"><span data-stu-id="62038-117">Yes</span></span> | 
<span data-ttu-id="62038-118">**CGI**</span><span class="sxs-lookup"><span data-stu-id="62038-118">**CGI**</span></span><br>`CgiModule` | <span data-ttu-id="62038-119">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-119">No</span></span> | 
<span data-ttu-id="62038-120">**구성 유효성 검사**</span><span class="sxs-lookup"><span data-stu-id="62038-120">**Configuration Validation**</span></span><br>`ConfigurationValidationModule` | <span data-ttu-id="62038-121">예</span><span class="sxs-lookup"><span data-stu-id="62038-121">Yes</span></span> | 
<span data-ttu-id="62038-122">**HTTP 오류**</span><span class="sxs-lookup"><span data-stu-id="62038-122">**HTTP Errors**</span></span><br>`CustomErrorModule` | <span data-ttu-id="62038-123">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-123">No</span></span> | [<span data-ttu-id="62038-124">상태 코드 페이지 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-124">Status Code Pages Middleware</span></span>](xref:fundamentals/error-handling#configuring-status-code-pages)
<span data-ttu-id="62038-125">**사용자 지정 로깅**</span><span class="sxs-lookup"><span data-stu-id="62038-125">**Custom Logging**</span></span><br>`CustomLoggingModule` | <span data-ttu-id="62038-126">예</span><span class="sxs-lookup"><span data-stu-id="62038-126">Yes</span></span> | 
<span data-ttu-id="62038-127">**기본 문서**</span><span class="sxs-lookup"><span data-stu-id="62038-127">**Default Document**</span></span><br>`DefaultDocumentModule` | <span data-ttu-id="62038-128">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-128">No</span></span> | [<span data-ttu-id="62038-129">기본 파일 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-129">Default Files Middleware</span></span>](xref:fundamentals/static-files#serve-a-default-document)
<span data-ttu-id="62038-130">**다이제스트 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-130">**Digest Authentication**</span></span><br>`DigestAuthenticationModule` | <span data-ttu-id="62038-131">예</span><span class="sxs-lookup"><span data-stu-id="62038-131">Yes</span></span> | 
<span data-ttu-id="62038-132">**디렉터리 검색**</span><span class="sxs-lookup"><span data-stu-id="62038-132">**Directory Browsing**</span></span><br>`DirectoryListingModule` | <span data-ttu-id="62038-133">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-133">No</span></span> | [<span data-ttu-id="62038-134">디렉터리 검색 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-134">Directory Browsing Middleware</span></span>](xref:fundamentals/static-files#enable-directory-browsing)
<span data-ttu-id="62038-135">**동적 압축**</span><span class="sxs-lookup"><span data-stu-id="62038-135">**Dynamic Compression**</span></span><br>`DynamicCompressionModule` | <span data-ttu-id="62038-136">예</span><span class="sxs-lookup"><span data-stu-id="62038-136">Yes</span></span> | [<span data-ttu-id="62038-137">응답 압축 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-137">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="62038-138">**추적**</span><span class="sxs-lookup"><span data-stu-id="62038-138">**Tracing**</span></span><br>`FailedRequestsTracingModule` | <span data-ttu-id="62038-139">예</span><span class="sxs-lookup"><span data-stu-id="62038-139">Yes</span></span> | [<span data-ttu-id="62038-140">ASP.NET Core Logging</span><span class="sxs-lookup"><span data-stu-id="62038-140">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index#the-tracesource-provider)
<span data-ttu-id="62038-141">**파일 캐싱**</span><span class="sxs-lookup"><span data-stu-id="62038-141">**File Caching**</span></span><br>`FileCacheModule` | <span data-ttu-id="62038-142">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-142">No</span></span> | [<span data-ttu-id="62038-143">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-143">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="62038-144">**HTTP 캐싱**</span><span class="sxs-lookup"><span data-stu-id="62038-144">**HTTP Caching**</span></span><br>`HttpCacheModule` | <span data-ttu-id="62038-145">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-145">No</span></span> | [<span data-ttu-id="62038-146">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-146">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="62038-147">**HTTP 로깅**</span><span class="sxs-lookup"><span data-stu-id="62038-147">**HTTP Logging**</span></span><br>`HttpLoggingModule` | <span data-ttu-id="62038-148">예</span><span class="sxs-lookup"><span data-stu-id="62038-148">Yes</span></span> | [<span data-ttu-id="62038-149">ASP.NET Core Logging</span><span class="sxs-lookup"><span data-stu-id="62038-149">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index)<br><span data-ttu-id="62038-150">구현: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span><span class="sxs-lookup"><span data-stu-id="62038-150">Implementations: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span></span>
<span data-ttu-id="62038-151">**HTTP 리디렉션**</span><span class="sxs-lookup"><span data-stu-id="62038-151">**HTTP Redirection**</span></span><br>`HttpRedirectionModule` | <span data-ttu-id="62038-152">예</span><span class="sxs-lookup"><span data-stu-id="62038-152">Yes</span></span> | [<span data-ttu-id="62038-153">URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="62038-154">**IIS 클라이언트 인증서 매핑 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-154">**IIS Client Certificate Mapping Authentication**</span></span><br>`IISCertificateMappingAuthenticationModule` | <span data-ttu-id="62038-155">예</span><span class="sxs-lookup"><span data-stu-id="62038-155">Yes</span></span> | 
<span data-ttu-id="62038-156">**IP 및 도메인 제한**</span><span class="sxs-lookup"><span data-stu-id="62038-156">**IP and Domain Restrictions**</span></span><br>`IpRestrictionModule` | <span data-ttu-id="62038-157">예</span><span class="sxs-lookup"><span data-stu-id="62038-157">Yes</span></span> | 
<span data-ttu-id="62038-158">**ISAPI 필터**</span><span class="sxs-lookup"><span data-stu-id="62038-158">**ISAPI Filters**</span></span><br>`IsapiFilterModule` | <span data-ttu-id="62038-159">예</span><span class="sxs-lookup"><span data-stu-id="62038-159">Yes</span></span> | [<span data-ttu-id="62038-160">미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-160">Middleware</span></span>](xref:fundamentals/middleware/index)
<span data-ttu-id="62038-161">**ISAPI**</span><span class="sxs-lookup"><span data-stu-id="62038-161">**ISAPI**</span></span><br>`IsapiModule` | <span data-ttu-id="62038-162">예</span><span class="sxs-lookup"><span data-stu-id="62038-162">Yes</span></span> | [<span data-ttu-id="62038-163">미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-163">Middleware</span></span>](xref:fundamentals/middleware/index)
<span data-ttu-id="62038-164">**프로토콜 지원**</span><span class="sxs-lookup"><span data-stu-id="62038-164">**Protocol Support**</span></span><br>`ProtocolSupportModule` | <span data-ttu-id="62038-165">예</span><span class="sxs-lookup"><span data-stu-id="62038-165">Yes</span></span> | 
<span data-ttu-id="62038-166">**요청 필터링**</span><span class="sxs-lookup"><span data-stu-id="62038-166">**Request Filtering**</span></span><br>`RequestFilteringModule` | <span data-ttu-id="62038-167">예</span><span class="sxs-lookup"><span data-stu-id="62038-167">Yes</span></span> | [<span data-ttu-id="62038-168">URL 다시 쓰기 미들웨어`IRule`</span><span class="sxs-lookup"><span data-stu-id="62038-168">URL Rewriting Middleware `IRule`</span></span>](xref:fundamentals/url-rewriting#irule-based-rule)
<span data-ttu-id="62038-169">**요청 모니터**</span><span class="sxs-lookup"><span data-stu-id="62038-169">**Request Monitor**</span></span><br>`RequestMonitorModule` | <span data-ttu-id="62038-170">예</span><span class="sxs-lookup"><span data-stu-id="62038-170">Yes</span></span> | 
<span data-ttu-id="62038-171">**URL 다시 쓰기**</span><span class="sxs-lookup"><span data-stu-id="62038-171">**URL Rewriting**</span></span><br>`RewriteModule` | <span data-ttu-id="62038-172">Yes†</span><span class="sxs-lookup"><span data-stu-id="62038-172">Yes†</span></span> | [<span data-ttu-id="62038-173">URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-173">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="62038-174">**SSI(SSI(Server Side Includes))**</span><span class="sxs-lookup"><span data-stu-id="62038-174">**Server Side Includes**</span></span><br>`ServerSideIncludeModule` | <span data-ttu-id="62038-175">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-175">No</span></span> | 
<span data-ttu-id="62038-176">**정적 압축**</span><span class="sxs-lookup"><span data-stu-id="62038-176">**Static Compression**</span></span><br>`StaticCompressionModule` | <span data-ttu-id="62038-177">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-177">No</span></span> | [<span data-ttu-id="62038-178">응답 압축 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-178">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="62038-179">**정적 콘텐츠**</span><span class="sxs-lookup"><span data-stu-id="62038-179">**Static Content**</span></span><br>`StaticFileModule` | <span data-ttu-id="62038-180">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-180">No</span></span> | [<span data-ttu-id="62038-181">정적 파일 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-181">Static File Middleware</span></span>](xref:fundamentals/static-files)
<span data-ttu-id="62038-182">**토큰 캐싱**</span><span class="sxs-lookup"><span data-stu-id="62038-182">**Token Caching**</span></span><br>`TokenCacheModule` | <span data-ttu-id="62038-183">예</span><span class="sxs-lookup"><span data-stu-id="62038-183">Yes</span></span> | 
<span data-ttu-id="62038-184">**URI 캐싱**</span><span class="sxs-lookup"><span data-stu-id="62038-184">**URI Caching**</span></span><br>`UriCacheModule` | <span data-ttu-id="62038-185">예</span><span class="sxs-lookup"><span data-stu-id="62038-185">Yes</span></span> | 
<span data-ttu-id="62038-186">**URL 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="62038-186">**URL Authorization**</span></span><br>`UrlAuthorizationModule` | <span data-ttu-id="62038-187">예</span><span class="sxs-lookup"><span data-stu-id="62038-187">Yes</span></span> | [<span data-ttu-id="62038-188">ASP.NET Core Identity</span><span class="sxs-lookup"><span data-stu-id="62038-188">ASP.NET Core Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="62038-189">**Windows 인증**</span><span class="sxs-lookup"><span data-stu-id="62038-189">**Windows Authentication**</span></span><br>`WindowsAuthenticationModule` | <span data-ttu-id="62038-190">예</span><span class="sxs-lookup"><span data-stu-id="62038-190">Yes</span></span> | 

<span data-ttu-id="62038-191">†The URL 재작성 모듈의 `isFile` 및 `isDirectory` 변경 때문에 ASP.NET Core 응용 프로그램을 사용 하지 않는 [디렉터리 구조](xref:host-and-deploy/directory-structure)합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-191">†The URL Rewrite Module's `isFile` and `isDirectory` don't work with ASP.NET Core apps due to the changes in [directory structure](xref:host-and-deploy/directory-structure).</span></span>

## <a name="managed-modules"></a><span data-ttu-id="62038-192">관리 되는 모듈</span><span class="sxs-lookup"><span data-stu-id="62038-192">Managed Modules</span></span>

<span data-ttu-id="62038-193">Module</span><span class="sxs-lookup"><span data-stu-id="62038-193">Module</span></span> | <span data-ttu-id="62038-194">.NET Core Active</span><span class="sxs-lookup"><span data-stu-id="62038-194">.NET Core Active</span></span> | <span data-ttu-id="62038-195">ASP.NET Core 옵션</span><span class="sxs-lookup"><span data-stu-id="62038-195">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="62038-196">AnonymousIdentification</span><span class="sxs-lookup"><span data-stu-id="62038-196">AnonymousIdentification</span></span> | <span data-ttu-id="62038-197">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-197">No</span></span> | 
<span data-ttu-id="62038-198">DefaultAuthentication</span><span class="sxs-lookup"><span data-stu-id="62038-198">DefaultAuthentication</span></span> | <span data-ttu-id="62038-199">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-199">No</span></span> | 
<span data-ttu-id="62038-200">FileAuthorization</span><span class="sxs-lookup"><span data-stu-id="62038-200">FileAuthorization</span></span> | <span data-ttu-id="62038-201">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-201">No</span></span> | 
<span data-ttu-id="62038-202">FormsAuthentication</span><span class="sxs-lookup"><span data-stu-id="62038-202">FormsAuthentication</span></span> | <span data-ttu-id="62038-203">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-203">No</span></span> | [<span data-ttu-id="62038-204">쿠키 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-204">Cookie Authentication Middleware</span></span>](xref:security/authentication/cookie)
<span data-ttu-id="62038-205">OutputCache</span><span class="sxs-lookup"><span data-stu-id="62038-205">OutputCache</span></span> | <span data-ttu-id="62038-206">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-206">No</span></span> | [<span data-ttu-id="62038-207">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-207">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="62038-208">프로필</span><span class="sxs-lookup"><span data-stu-id="62038-208">Profile</span></span> | <span data-ttu-id="62038-209">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-209">No</span></span> | 
<span data-ttu-id="62038-210">RoleManager</span><span class="sxs-lookup"><span data-stu-id="62038-210">RoleManager</span></span> | <span data-ttu-id="62038-211">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-211">No</span></span> | 
<span data-ttu-id="62038-212">ScriptModule-4.0</span><span class="sxs-lookup"><span data-stu-id="62038-212">ScriptModule-4.0</span></span> | <span data-ttu-id="62038-213">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-213">No</span></span> | 
<span data-ttu-id="62038-214">세션</span><span class="sxs-lookup"><span data-stu-id="62038-214">Session</span></span> | <span data-ttu-id="62038-215">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-215">No</span></span> | [<span data-ttu-id="62038-216">세션 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-216">Session Middleware</span></span>](xref:fundamentals/app-state)
<span data-ttu-id="62038-217">UrlAuthorization</span><span class="sxs-lookup"><span data-stu-id="62038-217">UrlAuthorization</span></span> | <span data-ttu-id="62038-218">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-218">No</span></span> | 
<span data-ttu-id="62038-219">UrlMappingsModule</span><span class="sxs-lookup"><span data-stu-id="62038-219">UrlMappingsModule</span></span> | <span data-ttu-id="62038-220">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-220">No</span></span> | [<span data-ttu-id="62038-221">URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="62038-221">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="62038-222">UrlRoutingModule-4.0</span><span class="sxs-lookup"><span data-stu-id="62038-222">UrlRoutingModule-4.0</span></span> | <span data-ttu-id="62038-223">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-223">No</span></span> | [<span data-ttu-id="62038-224">ASP.NET Core  Identity</span><span class="sxs-lookup"><span data-stu-id="62038-224">ASP.NET Core  Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="62038-225">WindowsAuthentication</span><span class="sxs-lookup"><span data-stu-id="62038-225">WindowsAuthentication</span></span> | <span data-ttu-id="62038-226">아니요</span><span class="sxs-lookup"><span data-stu-id="62038-226">No</span></span> | 

## <a name="iis-manager-application-changes"></a><span data-ttu-id="62038-227">IIS 관리자 응용 프로그램 변경</span><span class="sxs-lookup"><span data-stu-id="62038-227">IIS Manager application changes</span></span>

<span data-ttu-id="62038-228">IIS 관리자를 사용 하 여 설정을 구성 하는 *web.config* 앱의 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-228">Using IIS Manager to configure settings, the *web.config* file of the app is changed.</span></span> <span data-ttu-id="62038-229">응용 프로그램 배포 하는 경우 포함 하 여 *web.config*, IIS 관리자를 사용 하 여 변경 된 덮어씁니다가 배포 하 여 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-229">If deploying an app and including *web.config*, any changes made with IIS Manger are overwritten by the deployed *web.config* file.</span></span> <span data-ttu-id="62038-230">서버의 변경 되 면 *web.config* 파일, 업데이트 된 복사 *web.config* 파일을 즉시 로컬 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="62038-230">If changes are made to the server's *web.config* file, copy the updated *web.config* file to the local project immediately.</span></span>

## <a name="disabling-iis-modules"></a><span data-ttu-id="62038-231">IIS 모듈을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="62038-231">Disabling IIS modules</span></span>

<span data-ttu-id="62038-232">IIS 모듈 응용 프로그램에서는 응용 프로그램에 추가 된 항목에 대 한 사용 하지 않아야 하는 서버 수준에서 구성 된 경우 *web.config* 파일 모듈을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62038-232">If an IIS module is configured at the server level that must be disabled for an app, an addition to the app's *web.config* file can disable the module.</span></span> <span data-ttu-id="62038-233">모듈 위치에 그대로 둡니다 (있는 경우)에 구성 설정을 사용 하 여 비활성화 하거나 응용 프로그램에서 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-233">Either leave the module in place and deactivate it using a configuration setting (if available) or remove the module from the app.</span></span>

### <a name="module-deactivation"></a><span data-ttu-id="62038-234">모듈 비활성화</span><span class="sxs-lookup"><span data-stu-id="62038-234">Module deactivation</span></span>

<span data-ttu-id="62038-235">많은 모듈 수 있도록 하는 구성 설정에서 응용 프로그램을 제거 하지 않고 비활성화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-235">Many modules offer a configuration setting that allows them to be disabled them without removing them from the app.</span></span> <span data-ttu-id="62038-236">이것이 모듈을 비활성화 하려면 가장 간단 하 고 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-236">This is the simplest and quickest way to deactivate a module.</span></span> <span data-ttu-id="62038-237">예를 들어 IIS URL 재작성 모듈을 사용 하지 않도록 설정 하려면 사용 하 여는 `<httpRedirect>` 아래와 같이 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-237">For example if wishing to disable the IIS URL Rewrite Module, use the `<httpRedirect>` element as shown below.</span></span> <span data-ttu-id="62038-238">구성 설정 사용 하 여 모듈을 사용 하지 않도록 설정에 대 한 자세한 내용은 있는 링크는 *자식 요소* 섹션 [IIS `<system.webServer>` ](https://docs.microsoft.com/iis/configuration/system.webServer/)합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-238">For more information on disabling modules with configuration settings, follow the links in the *Child Elements* section of [IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/).</span></span>

```xml
<configuration>
  <system.webServer>
     <httpRedirect enabled="false" />
  </system.webServer>
</configuration>
```

### <a name="module-removal"></a><span data-ttu-id="62038-239">모듈 제거</span><span class="sxs-lookup"><span data-stu-id="62038-239">Module removal</span></span>

<span data-ttu-id="62038-240">설정을 사용 하 여 모듈을 제거 하도록 선택 하는 경우 *web.config*모듈의 잠금을 해제 하 고 잠금 해제는 `<modules>` 섹션 *web.config* 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-240">If opting to remove a module with a setting in *web.config*, unlock the module and unlock the `<modules>` section of *web.config* first.</span></span> <span data-ttu-id="62038-241">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62038-241">The steps are outlined below:</span></span>

1. <span data-ttu-id="62038-242">서버 수준에서 모듈의 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-242">Unlock the module at the server level.</span></span> <span data-ttu-id="62038-243">IIS 관리자에서 IIS 서버의 클릭 **연결** 사이드바 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-243">Click on the IIS server in the IIS Manager **Connections** sidebar.</span></span> <span data-ttu-id="62038-244">열기는 **모듈** 에 **IIS** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-244">Open the **Modules** in the **IIS** area.</span></span> <span data-ttu-id="62038-245">목록에 있는 모듈을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-245">Click on the module in the list.</span></span> <span data-ttu-id="62038-246">에 **동작** , 오른쪽에 클릭 **잠금 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-246">In the **Actions** sidebar on the right, click **Unlock**.</span></span> <span data-ttu-id="62038-247">많은 모듈에서 제거 하는 계획 된 대로 잠금 해제 *web.config* 나중입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-247">Unlock as many modules as are planned to remove from *web.config* later.</span></span>

2. <span data-ttu-id="62038-248">없이 앱을 배포는 `<modules>` 섹션 *web.config*합니다. 응용 프로그램으로 배포 하는 경우는 *web.config* 포함 하는 `<modules>` 섹션에 있는 섹션 잠금을 해제는 먼저 IIS 관리자에서 Configuration Manager는 섹션의 잠금을 해제 하려고 할 때 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-248">Deploy the app without a `<modules>` section in *web.config*. If an app is deployed with a *web.config* containing the `<modules>` section without having unlocked the section first in the IIS Manager, the Configuration Manager throws an exception when attempting to unlock the section.</span></span> <span data-ttu-id="62038-249">따라서 없이 앱을 배포는 `<modules>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="62038-249">Therefore, deploy the app without a `<modules>` section.</span></span>

3. <span data-ttu-id="62038-250">잠금 해제는 `<modules>` 섹션 *web.config*합니다. 에 **연결** 사이드바에서 웹 사이트를 클릭 **사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-250">Unlock the `<modules>` section of *web.config*. In the **Connections** sidebar, click the website in **Sites**.</span></span> <span data-ttu-id="62038-251">에 **관리** 영역을 열고는 **구성 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-251">In the **Management** area, open the **Configuration Editor**.</span></span> <span data-ttu-id="62038-252">탐색 컨트롤을 사용 하 여 선택 된 `system.webServer/modules` 섹션.</span><span class="sxs-lookup"><span data-stu-id="62038-252">Use the navigation controls to select the `system.webServer/modules` section.</span></span> <span data-ttu-id="62038-253">에 **동작** 를 클릭 하 여, 오른쪽에 **잠금 해제** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-253">In the **Actions** sidebar on the right, click to **Unlock** the section.</span></span>

4. <span data-ttu-id="62038-254">이 시점에서 `<modules>` 섹션에 추가할 수는 *web.config* 파일는 `<remove>` 요소를 응용 프로그램에서 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-254">At this point, a `<modules>` section can be added to the *web.config* file with a `<remove>` element to remove the module from the app.</span></span> <span data-ttu-id="62038-255">여러 `<remove>` 여러 모듈을 제거 하는 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62038-255">Multiple `<remove>` elements can be added to remove multiple modules.</span></span> <span data-ttu-id="62038-256">경우 반드시 *web.config* 프로젝트를 로컬에서 즉시 확인 하는 서버에서 정의가 변경 되어도 합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-256">Don't forget that if *web.config* changes are made on the server to make them immediately in the project locally.</span></span> <span data-ttu-id="62038-257">이러한 방식으로 모듈을 제거 하면 서버에서 다른 앱을 사용 하 여 모듈의 사용을 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62038-257">Removing a module this way won't affect the use of the module with other apps on the server.</span></span>

  ```xml
  <configuration> 
    <system.webServer> 
      <modules> 
        <remove name="MODULE_NAME" /> 
      </modules> 
    </system.webServer> 
  </configuration>
  ```

<span data-ttu-id="62038-258">설치 된 기본 모듈로 IIS 설치의 경우 다음을 사용 하 여 `<module>` 기본 모듈을 제거 하려면 섹션.</span><span class="sxs-lookup"><span data-stu-id="62038-258">For an IIS installation with the default modules installed, use the following `<module>` section to remove the default modules.</span></span>

```xml
<modules>
  <remove name="CustomErrorModule" />
  <remove name="DefaultDocumentModule" />
  <remove name="DirectoryListingModule" />
  <remove name="HttpCacheModule" />
  <remove name="HttpLoggingModule" />
  <remove name="ProtocolSupportModule" />
  <remove name="RequestFilteringModule" />
  <remove name="StaticCompressionModule" /> 
  <remove name="StaticFileModule" /> 
</modules>
```

<span data-ttu-id="62038-259">와 IIS 모듈을 제거할 수도 있습니다 *Appcmd.exe*합니다.</span><span class="sxs-lookup"><span data-stu-id="62038-259">An IIS module can also be removed with *Appcmd.exe*.</span></span> <span data-ttu-id="62038-260">제공 된 `MODULE_NAME` 및 `APPLICATION_NAME` 아래에 표시 된 명령에서:</span><span class="sxs-lookup"><span data-stu-id="62038-260">Provide the `MODULE_NAME` and `APPLICATION_NAME` in the command shown below:</span></span>

```console
Appcmd.exe delete module MODULE_NAME /app.name:APPLICATION_NAME
```

<span data-ttu-id="62038-261">다음은 제거 하는 방법의 `DynamicCompressionModule` 기본 웹 사이트에서:</span><span class="sxs-lookup"><span data-stu-id="62038-261">Here's how to remove the `DynamicCompressionModule` from the Default Web Site:</span></span>

```console
%windir%\system32\inetsrv\appcmd.exe delete module DynamicCompressionModule /app.name:"Default Web Site"
```

## <a name="minimum-module-configuration"></a><span data-ttu-id="62038-262">최소 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="62038-262">Minimum module configuration</span></span>

<span data-ttu-id="62038-263">ASP.NET Core 응용 프로그램을 실행 하는 데 필요한 유일한 모듈은 익명 인증 모듈 및 ASP.NET Core 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="62038-263">The only modules required to run an ASP.NET Core app are the Anonymous Authentication Module and the ASP.NET Core Module.</span></span>

![표시 된 최소 모듈 구성을 사용 하 여 모듈에 IIS 관리자를 열려면](modules/_static/modules.png)

## <a name="additional-resources"></a><span data-ttu-id="62038-265">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="62038-265">Additional resources</span></span>

* [<span data-ttu-id="62038-266">IIS를 사용하여 Windows에서 호스트</span><span class="sxs-lookup"><span data-stu-id="62038-266">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="62038-267">IIS 모듈 개요</span><span class="sxs-lookup"><span data-stu-id="62038-267">IIS Modules Overview</span></span>](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
* [<span data-ttu-id="62038-268">IIS 7.0 역할 및 모듈을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="62038-268">Customizing IIS 7.0 Roles and Modules</span></span>](https://technet.microsoft.com/library/cc627313.aspx)
* [<span data-ttu-id="62038-269">IIS `<system.webServer>`</span><span class="sxs-lookup"><span data-stu-id="62038-269">IIS `<system.webServer>`</span></span>](https://docs.microsoft.com/iis/configuration/system.webServer/)
