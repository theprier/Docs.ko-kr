---
title: "ASP.NET Core 보안 개요 | Microsoft Docs"
author: rachelappel
description: "ASP.NET Core의 인증, 권한 부여 및 보안 기본 사항 알아보기"
ms.author: rachelap
manager: wpickett
ms.date: 11/01/2017
ms.topic: article
ms.assetid: a8fb7eb7-e0e5-4394-84f3-1f1dbe012345
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/index
ms.openlocfilehash: 3f4df08d6cf5d183735ae4b4ec4f07ed60a9623a
ms.sourcegitcommit: f1436107b4c022b26f5235dddef103cec5aa6bff
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2017
---
# <a name="aspnet-core-security-overview"></a>ASP.NET Core 보안 개요

개발자는 ASP.NET Core를 사용하여 앱의 보안을 간편하게 구성 및 관리할 수 있습니다. ASP.NET Core는 인증, 권한 부여, 데이터 보호, SSL 적용, 앱 비밀, 요청 위조 방지 및 CORS 관리를 위한 기능을 포함하고 있습니다. 이러한 보안 기능을 사용하여 강력하면서도 안전한 ASP.NET Core 앱을 빌드할 수 있습니다. 

## <a name="aspnet-core-security-features"></a>ASP.NET Core 보안 기능

ASP.NET Core는 기본 제공 ID 공급자를 포함하여 앱을 보호하는 여러 도구와 라이브러리를 제공하지만 Facebook, Twitter, LinkedIn 등의 타사 ID 서비스를 사용할 수도 있습니다. ASP.NET Core를 사용하면 기밀 정보를 코드에 노출할 필요 없이 저장하고 사용할 수 있는 방법인 앱 비밀을 간편하게 관리할 수 있습니다. 

## <a name="authentication-vs-authorization"></a>인증 vs. 권한 부여

인증은 사용자가 자격 증명을 제공하면 운영 체제, 데이터베이스, 앱 또는 리소스에 저장된 자격 증명과 비교하는 프로세스입니다. 두 자격 증명이 일치하면 사용자 인증이 성공하고 사용자는 권한 부여 프로세스 동안 권한이 부여된 작업을 수행할 수 있습니다. 권한 부여는 사용자가 할 수 있는 작업을 결정하는 프로세스를 말합니다. 

인증을 이해하기 위한 또 다른 개념으로 서버, 데이터베이스, 앱, 리소스 등의 공간에 들어가는 것으로 생각할 수 있고, 권한 부여는 사용자가 해당 공간(서버, 데이터베이스 또는 앱) 내에서 어떤 개체에 대해 어떤 작업을 수행할 수 있는지 결정하는 것입니다.

## <a name="common-vulnerabilities-in-software"></a>소프트웨어의 일반적인 취약점

ASP.NET Core 및 EF는 앱을 보호하고 보안 위반을 방지하는 기능을 포함하고 있습니다. 다음 링크 목록을 선택하면 웹앱의 가장 일반적인 보안 취약점을 방지하는 기술을 구체적으로 설명하는 문서로 이동합니다.

* [사이트 간 스크립팅 공격](https://docs.microsoft.com/aspnet/core/security/cross-site-scripting)
* [SQL 삽입 공격](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [CSRF(사이트 간 요청 위조)](https://docs.microsoft.com/aspnet/core/security/anti-request-forgery)
* [오픈 리디렉션 공격](https://docs.microsoft.com/aspnet/core/security/preventing-open-redirects)

그 외에도 알고 계셔야 하는 취약점이 더 있습니다. 자세한 내용은 이 문서의 *ASP.NET 보안 설명서*에 대한 섹션을 참조하세요. 

## <a name="aspnet-security-documentation"></a>ASP.NET 보안 설명서

*   [인증](authentication/index.md)
    *   [ID 소개](authentication/identity.md)
    *   [Facebook, Google 및 기타 외부 공급자를 통해 인증 사용](authentication/social/index.md)
    * [Windows 인증 구성](authentication/windowsauth.md)
    *   [계정 확인 및 암호 복구](authentication/accconfirm.md)
    *   [SMS를 사용한 2단계 인증](authentication/2fa.md) 
    *   [ASP.NET Core ID 없이 쿠키 인증 사용](authentication/cookie.md)
    *   [Azure Active Directory](authentication/azure-active-directory/index.md)
        *   [ASP.NET Core 웹앱에 Azure AD 통합](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [Azure AD를 사용하여 WPF 응용 프로그램에서 ASP.NET Core Web API 호출](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [Azure AD를 사용하여 ASP.NET Core 웹 응용 프로그램에서 Web API 호출](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [Azure AD B2C를 사용하여 ASP.NET Core 웹앱](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [IdentityServer4를 사용하여 ASP.NET Core 앱 보호](https://identityserver4.readthedocs.io)
*   [권한 부여](authorization/index.md)
    *   [소개](authorization/introduction.md)
    *   [권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기](xref:security/authorization/secure-data)
    *   [단순 권한 부여](authorization/simple.md)
    *   [역할 기반 권한 부여](authorization/roles.md)
    *   [클레임 기반 권한 부여](authorization/claims.md)
    *   [사용자 지정 정책 기반 권한 부여](authorization/policies.md)
    *   [요구 사항 처리기의 종속성 주입](authorization/dependencyinjection.md)
    *   [리소스 기반 권한 부여](authorization/resourcebased.md)
    *   [보기 기반 권한 부여](authorization/views.md)
    *   [구성표로 ID 제한](authorization/limitingidentitybyscheme.md)
*   [데이터 보호](data-protection/index.md)
    *   [데이터 보호 소개](data-protection/introduction.md)
    *   [데이터 보호 API 시작](data-protection/using-data-protection.md)
    *   [소비자 API](data-protection/consumer-apis/index.md)
        *   [소비자 API 개요](data-protection/consumer-apis/overview.md)
        *   [용도 문자열](data-protection/consumer-apis/purpose-strings.md)
        *   [용도 계층 구조 및 다중 테넌트](data-protection/consumer-apis/purpose-strings-multitenancy.md)
        *   [암호 해시](data-protection/consumer-apis/password-hashing.md)
        *   [보호된 페이로드의 수명 제한](data-protection/consumer-apis/limited-lifetime-payloads.md)
        *   [호출된 키가 속한 페이로드 보호 해제](data-protection/consumer-apis/dangerous-unprotect.md)
    *   [구성](data-protection/configuration/index.md)
        *   [데이터 보호 구성](data-protection/configuration/overview.md)
        *   [기본 설정](data-protection/configuration/default-settings.md)
        *   [컴퓨터 수준 정책](data-protection/configuration/machine-wide-policy.md)
        *   [비 DI 인식 시나리오](data-protection/configuration/non-di-scenarios.md)
    *   [확장성 API](data-protection/extensibility/index.md)
        *   [Core 암호화 확장성](data-protection/extensibility/core-crypto.md)
        *   [키 관리 확장성](data-protection/extensibility/key-management.md)
        *   [기타 API](data-protection/extensibility/misc-apis.md)
    *   [구현](data-protection/implementation/index.md)
        *   [인증된 암호화 세부 정보](data-protection/implementation/authenticated-encryption-details.md)
        *   [하위 키 파생 및 인증된 암호화](data-protection/implementation/subkeyderivation.md)
        *   [컨텍스트 헤더](data-protection/implementation/context-headers.md)
        *   [키 관리](data-protection/implementation/key-management.md)
        *   [키 저장소 공급자](data-protection/implementation/key-storage-providers.md)
        *   [미사용 키 암호화](data-protection/implementation/key-encryption-at-rest.md)
        *   [키 불변성 및 설정 변경](data-protection/implementation/key-immutability.md)
        *   [키 저장소 형식](data-protection/implementation/key-storage-format.md)
        *   [삭제되는 데이터 보호 공급자](data-protection/implementation/key-storage-ephemeral.md)
    *   [호환성](data-protection/compatibility/index.md)
        *   [응용프로그램 쿠키 공유](data-protection/compatibility/cookie-sharing.md)
        *   [ASP.NET에서 <machineKey> 바꾸기](data-protection/compatibility/replacing-machinekey.md)
*   [권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기](xref:security/authorization/secure-data)
*   [개발 중 안전한 앱 비밀 저장소](app-secrets.md)
*   [Azure Key Vault 구성 공급자](key-vault-configuration.md)
*   [SSL 적용](enforcing-ssl.md)
*   [요청 위조 방지](anti-request-forgery.md)
*   [오픈 리디렉션(Open Redirect) 공격 방지](preventing-open-redirects.md)
*   [교차 사이트 스크립팅 방지](cross-site-scripting.md)
*   [원본 간 요청(CORS) 사용](cors.md)
