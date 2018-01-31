---
title: "ASP.NET Core 보안 개요"
author: rachelappel
description: "ASP.NET Core의 인증, 권한 부여 및 보안 기본 사항에 대해 알아봅니다."
manager: wpickett
ms.author: rachelap
ms.date: 11/01/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/index
ms.openlocfilehash: e1aaae09fe69e6b65a917785b436f927fac5345d
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="aspnet-core-security-overview"></a><span data-ttu-id="7dbe2-103">ASP.NET Core 보안 개요</span><span class="sxs-lookup"><span data-stu-id="7dbe2-103">ASP.NET Core Security Overview</span></span>

<span data-ttu-id="7dbe2-104">개발자는 ASP.NET Core를 사용하여 앱의 보안을 간편하게 구성 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-104">ASP.NET Core enables developers to easily configure and manage security for their apps.</span></span> <span data-ttu-id="7dbe2-105">ASP.NET Core는 인증, 권한 부여, 데이터 보호, SSL 적용, 앱 비밀, 요청 위조 방지 및 CORS 관리를 위한 기능을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-105">ASP.NET Core contains features for managing authentication, authorization, data protection, SSL enforcement, app secrets, anti-request forgery protection, and CORS management.</span></span> <span data-ttu-id="7dbe2-106">이러한 보안 기능을 사용하여 강력하면서도 안전한 ASP.NET Core 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-106">These security features allow you to build robust yet secure ASP.NET Core apps.</span></span> 

## <a name="aspnet-core-security-features"></a><span data-ttu-id="7dbe2-107">ASP.NET Core 보안 기능</span><span class="sxs-lookup"><span data-stu-id="7dbe2-107">ASP.NET Core security features</span></span>

<span data-ttu-id="7dbe2-108">ASP.NET Core는 기본 제공 ID 공급자를 포함하여 앱을 보호하는 여러 도구와 라이브러리를 제공하지만 Facebook, Twitter, LinkedIn 등의 타사 ID 서비스를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-108">ASP.NET Core provides many tools and libraries to secure your apps including built-in Identity providers but you can use 3rd party identity services such as Facebook, Twitter, or LinkedIn.</span></span> <span data-ttu-id="7dbe2-109">ASP.NET Core를 사용하면 기밀 정보를 코드에 노출할 필요 없이 저장하고 사용할 수 있는 방법인 앱 비밀을 간편하게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-109">With ASP.NET Core, you can easily manage app secrets, which are a way to store and use confidential information without having to expose it in the code.</span></span> 

## <a name="authentication-vs-authorization"></a><span data-ttu-id="7dbe2-110">인증 vs. 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-110">Authentication vs. Authorization</span></span>

<span data-ttu-id="7dbe2-111">인증은 사용자가 자격 증명을 제공하면 운영 체제, 데이터베이스, 앱 또는 리소스에 저장된 자격 증명과 비교하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-111">Authentication is a process in which a user provides credentials that are then compared to those stored in an operating system, database, app or resource.</span></span> <span data-ttu-id="7dbe2-112">두 자격 증명이 일치하면 사용자 인증이 성공하고 사용자는 권한 부여 프로세스 동안 권한이 부여된 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-112">If they match, users authenticate successfully, and can then perform actions that they're authorized for, during an authorization process.</span></span> <span data-ttu-id="7dbe2-113">권한 부여는 사용자가 할 수 있는 작업을 결정하는 프로세스를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-113">The authorization refers to the process that determines what a user is allowed to do.</span></span> 

<span data-ttu-id="7dbe2-114">인증을 이해하기 위한 또 다른 개념으로 서버, 데이터베이스, 앱, 리소스 등의 공간에 들어가는 것으로 생각할 수 있고, 권한 부여는 사용자가 해당 공간(서버, 데이터베이스 또는 앱) 내에서 어떤 개체에 대해 어떤 작업을 수행할 수 있는지 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-114">Another way to think of authentication is to consider it as a way to enter a space, such as a server, database, app or resource, while authorization is which actions the user can perform to which objects inside that space (server, database, or app).</span></span>

## <a name="common-vulnerabilities-in-software"></a><span data-ttu-id="7dbe2-115">소프트웨어의 일반적인 취약점</span><span class="sxs-lookup"><span data-stu-id="7dbe2-115">Common Vulnerabilities in software</span></span>

<span data-ttu-id="7dbe2-116">ASP.NET Core 및 EF는 앱을 보호하고 보안 위반을 방지하는 기능을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-116">ASP.NET Core and EF contain features that help you secure your apps and prevent security breaches.</span></span> <span data-ttu-id="7dbe2-117">다음 링크 목록을 선택하면 웹앱의 가장 일반적인 보안 취약점을 방지하는 기술을 구체적으로 설명하는 문서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-117">The following list of links takes you to documentation detailing techniques to avoid the most common security vulnerabilities in web apps:</span></span>

* [<span data-ttu-id="7dbe2-118">사이트 간 스크립팅 공격</span><span class="sxs-lookup"><span data-stu-id="7dbe2-118">Cross-site scripting attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/cross-site-scripting)
* [<span data-ttu-id="7dbe2-119">SQL 삽입 공격</span><span class="sxs-lookup"><span data-stu-id="7dbe2-119">SQL injection attacks</span></span>](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [<span data-ttu-id="7dbe2-120">CSRF(사이트 간 요청 위조)</span><span class="sxs-lookup"><span data-stu-id="7dbe2-120">Cross-Site Request Forgery (CSRF)</span></span>](https://docs.microsoft.com/aspnet/core/security/anti-request-forgery)
* [<span data-ttu-id="7dbe2-121">오픈 리디렉션 공격</span><span class="sxs-lookup"><span data-stu-id="7dbe2-121">Open redirect attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/preventing-open-redirects)

<span data-ttu-id="7dbe2-122">그 외에도 알고 계셔야 하는 취약점이 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-122">There are more vulnerabilities that you should be aware of.</span></span> <span data-ttu-id="7dbe2-123">자세한 내용은 이 문서의 *ASP.NET 보안 설명서*에 대한 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7dbe2-123">For more information, see the section in this document on *ASP.NET Security Documentation*.</span></span> 

## <a name="aspnet-security-documentation"></a><span data-ttu-id="7dbe2-124">ASP.NET 보안 설명서</span><span class="sxs-lookup"><span data-stu-id="7dbe2-124">ASP.NET Security Documentation</span></span>

*   [<span data-ttu-id="7dbe2-125">인증</span><span class="sxs-lookup"><span data-stu-id="7dbe2-125">Authentication</span></span>](authentication/index.md)
    *   [<span data-ttu-id="7dbe2-126">ID 소개</span><span class="sxs-lookup"><span data-stu-id="7dbe2-126">Introduction to Identity</span></span>](authentication/identity.md)
    *   [<span data-ttu-id="7dbe2-127">Facebook, Google 및 기타 외부 공급자를 통해 인증 사용</span><span class="sxs-lookup"><span data-stu-id="7dbe2-127">Enable authentication using Facebook, Google, and other external providers</span></span>](authentication/social/index.md)
    * [<span data-ttu-id="7dbe2-128">Windows 인증 구성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-128">Configure Windows Authentication</span></span>](authentication/windowsauth.md)
    *   [<span data-ttu-id="7dbe2-129">계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="7dbe2-129">Account confirmation and password recovery</span></span>](authentication/accconfirm.md)
    *   [<span data-ttu-id="7dbe2-130">SMS를 사용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="7dbe2-130">Two-factor authentication with SMS</span></span>](authentication/2fa.md) 
    *   [<span data-ttu-id="7dbe2-131">ID 없이 쿠키 인증 사용</span><span class="sxs-lookup"><span data-stu-id="7dbe2-131">Use cookie authentication without Identity</span></span>](authentication/cookie.md)
    *   [<span data-ttu-id="7dbe2-132">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dbe2-132">Azure Active Directory</span></span>](authentication/azure-active-directory/index.md)
        *   [<span data-ttu-id="7dbe2-133">ASP.NET Core 웹앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="7dbe2-133">Integrate Azure AD into an ASP.NET Core web app</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="7dbe2-134">Azure AD를 사용하여 WPF 앱에서 ASP.NET Core Web API 호출</span><span class="sxs-lookup"><span data-stu-id="7dbe2-134">Call an ASP.NET Core Web API from a WPF app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [<span data-ttu-id="7dbe2-135">Azure AD를 사용하여 ASP.NET Core 웹앱에서 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="7dbe2-135">Call a Web API in an ASP.NET Core web app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="7dbe2-136">Azure AD B2C를 사용하여 ASP.NET Core 웹앱</span><span class="sxs-lookup"><span data-stu-id="7dbe2-136">An ASP.NET Core web app with Azure AD B2C</span></span>](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [<span data-ttu-id="7dbe2-137">IdentityServer4를 사용하여 ASP.NET Core 앱 보호</span><span class="sxs-lookup"><span data-stu-id="7dbe2-137">Secure ASP.NET Core apps with IdentityServer4</span></span>](https://identityserver4.readthedocs.io)
*   [<span data-ttu-id="7dbe2-138">권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-138">Authorization</span></span>](authorization/index.md)
    *   [<span data-ttu-id="7dbe2-139">소개</span><span class="sxs-lookup"><span data-stu-id="7dbe2-139">Introduction</span></span>](authorization/introduction.md)
    *   [<span data-ttu-id="7dbe2-140">권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7dbe2-140">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
    *   [<span data-ttu-id="7dbe2-141">단순 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-141">Simple authorization</span></span>](authorization/simple.md)
    *   [<span data-ttu-id="7dbe2-142">역할 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-142">Role-based authorization</span></span>](authorization/roles.md)
    *   [<span data-ttu-id="7dbe2-143">클레임 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-143">Claims-based authorization</span></span>](authorization/claims.md)
    *   [<span data-ttu-id="7dbe2-144">정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-144">Policy-based authorization</span></span>](authorization/policies.md)
    *   [<span data-ttu-id="7dbe2-145">요구 사항 처리기의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="7dbe2-145">Dependency injection in requirement handlers</span></span>](authorization/dependencyinjection.md)
    *   [<span data-ttu-id="7dbe2-146">리소스 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-146">Resource-based authorization</span></span>](authorization/resourcebased.md)
    *   [<span data-ttu-id="7dbe2-147">보기 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7dbe2-147">View-based authorization</span></span>](authorization/views.md)
    *   [<span data-ttu-id="7dbe2-148">구성표로 ID 제한</span><span class="sxs-lookup"><span data-stu-id="7dbe2-148">Limit identity by scheme</span></span>](authorization/limitingidentitybyscheme.md)
*   [<span data-ttu-id="7dbe2-149">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="7dbe2-149">Data protection</span></span>](data-protection/index.md)
    *   [<span data-ttu-id="7dbe2-150">데이터 보호 소개</span><span class="sxs-lookup"><span data-stu-id="7dbe2-150">Introduction to data protection</span></span>](data-protection/introduction.md)
    *   [<span data-ttu-id="7dbe2-151">데이터 보호 API 시작</span><span class="sxs-lookup"><span data-stu-id="7dbe2-151">Get started with the Data Protection APIs</span></span>](data-protection/using-data-protection.md)
    *   [<span data-ttu-id="7dbe2-152">소비자 API</span><span class="sxs-lookup"><span data-stu-id="7dbe2-152">Consumer APIs</span></span>](data-protection/consumer-apis/index.md)
        *   [<span data-ttu-id="7dbe2-153">소비자 API 개요</span><span class="sxs-lookup"><span data-stu-id="7dbe2-153">Consumer APIs Overview</span></span>](data-protection/consumer-apis/overview.md)
        *   [<span data-ttu-id="7dbe2-154">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="7dbe2-154">Purpose strings</span></span>](data-protection/consumer-apis/purpose-strings.md)
        *   [<span data-ttu-id="7dbe2-155">용도 계층 구조 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="7dbe2-155">Purpose hierarchy and multi-tenancy</span></span>](data-protection/consumer-apis/purpose-strings-multitenancy.md)
        *   [<span data-ttu-id="7dbe2-156">암호 해시</span><span class="sxs-lookup"><span data-stu-id="7dbe2-156">Password hashing</span></span>](data-protection/consumer-apis/password-hashing.md)
        *   [<span data-ttu-id="7dbe2-157">보호된 페이로드의 수명 제한</span><span class="sxs-lookup"><span data-stu-id="7dbe2-157">Limit the lifetime of protected payloads</span></span>](data-protection/consumer-apis/limited-lifetime-payloads.md)
        *   [<span data-ttu-id="7dbe2-158">호출된 키가 속한 페이로드 보호 해제</span><span class="sxs-lookup"><span data-stu-id="7dbe2-158">Unprotect payloads whose keys have been revoked</span></span>](data-protection/consumer-apis/dangerous-unprotect.md)
    *   [<span data-ttu-id="7dbe2-159">구성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-159">Configuration</span></span>](data-protection/configuration/index.md)
        *   [<span data-ttu-id="7dbe2-160">데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-160">Configure data protection</span></span>](data-protection/configuration/overview.md)
        *   [<span data-ttu-id="7dbe2-161">기본 설정</span><span class="sxs-lookup"><span data-stu-id="7dbe2-161">Default settings</span></span>](data-protection/configuration/default-settings.md)
        *   [<span data-ttu-id="7dbe2-162">컴퓨터 수준의 정책</span><span class="sxs-lookup"><span data-stu-id="7dbe2-162">Machine-wide policy</span></span>](data-protection/configuration/machine-wide-policy.md)
        *   [<span data-ttu-id="7dbe2-163">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="7dbe2-163">Non DI-aware scenarios</span></span>](data-protection/configuration/non-di-scenarios.md)
    *   [<span data-ttu-id="7dbe2-164">확장성 API</span><span class="sxs-lookup"><span data-stu-id="7dbe2-164">Extensibility APIs</span></span>](data-protection/extensibility/index.md)
        *   [<span data-ttu-id="7dbe2-165">Core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-165">Core cryptography extensibility</span></span>](data-protection/extensibility/core-crypto.md)
        *   [<span data-ttu-id="7dbe2-166">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-166">Key management extensibility</span></span>](data-protection/extensibility/key-management.md)
        *   [<span data-ttu-id="7dbe2-167">기타 API</span><span class="sxs-lookup"><span data-stu-id="7dbe2-167">Miscellaneous APIs</span></span>](data-protection/extensibility/misc-apis.md)
    *   [<span data-ttu-id="7dbe2-168">구현</span><span class="sxs-lookup"><span data-stu-id="7dbe2-168">Implementation</span></span>](data-protection/implementation/index.md)
        *   [<span data-ttu-id="7dbe2-169">인증된 암호화 세부 정보</span><span class="sxs-lookup"><span data-stu-id="7dbe2-169">Authenticated encryption details</span></span>](data-protection/implementation/authenticated-encryption-details.md)
        *   [<span data-ttu-id="7dbe2-170">하위 키 파생 및 인증된 암호화</span><span class="sxs-lookup"><span data-stu-id="7dbe2-170">Subkey derivation and authenticated encryption</span></span>](data-protection/implementation/subkeyderivation.md)
        *   [<span data-ttu-id="7dbe2-171">컨텍스트 헤더</span><span class="sxs-lookup"><span data-stu-id="7dbe2-171">Context headers</span></span>](data-protection/implementation/context-headers.md)
        *   [<span data-ttu-id="7dbe2-172">키 관리</span><span class="sxs-lookup"><span data-stu-id="7dbe2-172">Key management</span></span>](data-protection/implementation/key-management.md)
        *   [<span data-ttu-id="7dbe2-173">키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="7dbe2-173">Key storage providers</span></span>](data-protection/implementation/key-storage-providers.md)
        *   [<span data-ttu-id="7dbe2-174">미사용 키 암호화</span><span class="sxs-lookup"><span data-stu-id="7dbe2-174">Key encryption at rest</span></span>](data-protection/implementation/key-encryption-at-rest.md)
        *   [<span data-ttu-id="7dbe2-175">키 불변성 및 설정 변경</span><span class="sxs-lookup"><span data-stu-id="7dbe2-175">Key immutability and changing settings</span></span>](data-protection/implementation/key-immutability.md)
        *   [<span data-ttu-id="7dbe2-176">키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="7dbe2-176">Key storage format</span></span>](data-protection/implementation/key-storage-format.md)
        *   [<span data-ttu-id="7dbe2-177">삭제되는 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="7dbe2-177">Ephemeral data protection providers</span></span>](data-protection/implementation/key-storage-ephemeral.md)
    *   [<span data-ttu-id="7dbe2-178">호환성</span><span class="sxs-lookup"><span data-stu-id="7dbe2-178">Compatibility</span></span>](data-protection/compatibility/index.md)
        *   [<span data-ttu-id="7dbe2-179">앱 간 쿠키 공유</span><span class="sxs-lookup"><span data-stu-id="7dbe2-179">Share cookies among apps</span></span>](data-protection/compatibility/cookie-sharing.md)
        *   [<span data-ttu-id="7dbe2-180">ASP.NET에서 <machineKey> 바꾸기</span><span class="sxs-lookup"><span data-stu-id="7dbe2-180">Replace <machineKey> in ASP.NET</span></span>](data-protection/compatibility/replacing-machinekey.md)
*   [<span data-ttu-id="7dbe2-181">권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7dbe2-181">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
*   [<span data-ttu-id="7dbe2-182">개발 중 안전한 앱 비밀 저장소</span><span class="sxs-lookup"><span data-stu-id="7dbe2-182">Safe storage of app secrets during development</span></span>](app-secrets.md)
*   [<span data-ttu-id="7dbe2-183">Azure Key Vault 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="7dbe2-183">Azure Key Vault configuration provider</span></span>](key-vault-configuration.md)
*   [<span data-ttu-id="7dbe2-184">SSL 적용</span><span class="sxs-lookup"><span data-stu-id="7dbe2-184">Enforce SSL</span></span>](enforcing-ssl.md)
*   [<span data-ttu-id="7dbe2-185">요청 위조 방지</span><span class="sxs-lookup"><span data-stu-id="7dbe2-185">Anti-Request Forgery</span></span>](anti-request-forgery.md)
*   [<span data-ttu-id="7dbe2-186">오픈 리디렉션 공격 방지</span><span class="sxs-lookup"><span data-stu-id="7dbe2-186">Prevent open redirect attacks</span></span>](preventing-open-redirects.md)
*   [<span data-ttu-id="7dbe2-187">사이트 간 스크립팅 방지</span><span class="sxs-lookup"><span data-stu-id="7dbe2-187">Prevent Cross-Site Scripting</span></span>](cross-site-scripting.md)
*   [<span data-ttu-id="7dbe2-188">원본 간 요청(CORS) 사용</span><span class="sxs-lookup"><span data-stu-id="7dbe2-188">Enable Cross-Origin Requests (CORS)</span></span>](cors.md)
