---
title: ASP.NET Core 보안 개요
author: tdykstra
description: ASP.NET Core의 인증, 권한 부여 및 보안 기본 사항에 대해 알아봅니다.
ms.author: tdykstra
ms.date: 11/01/2017
uid: security/index
ms.openlocfilehash: 3a1c1ea1ad28fccbe5ae91b0be193938b095f60b
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41746091"
---
# <a name="overview-of-aspnet-core-security"></a>ASP.NET Core 보안 개요

개발자는 ASP.NET Core를 사용하여 앱의 보안을 간편하게 구성 및 관리할 수 있습니다. ASP.NET Core는 인증, 권한 부여, 데이터 보호, SSL 적용, 앱 비밀, 요청 위조 방지 및 CORS 관리를 위한 기능을 포함하고 있습니다. 이러한 보안 기능을 사용하여 강력하면서도 안전한 ASP.NET Core 앱을 빌드할 수 있습니다.

## <a name="aspnet-core-security-features"></a>ASP.NET Core 보안 기능

ASP.NET Core는 기본 제공 ID 공급자를 포함하여 앱을 보호하는 여러 도구와 라이브러리를 제공하지만 Facebook, Twitter, LinkedIn 등의 타사 ID 서비스를 사용할 수도 있습니다. ASP.NET Core를 사용하면 기밀 정보를 코드에 노출할 필요 없이 저장하고 사용할 수 있는 방법인 앱 비밀을 간편하게 관리할 수 있습니다.

## <a name="authentication-vs-authorization"></a>인증 vs. 권한 부여

인증은 사용자가 자격 증명을 제공하면 운영 체제, 데이터베이스, 앱 또는 리소스에 저장된 자격 증명과 비교하는 프로세스입니다. 두 자격 증명이 일치하면 사용자 인증이 성공하고 사용자는 권한 부여 프로세스 동안 권한이 부여된 작업을 수행할 수 있습니다. 권한 부여는 사용자가 할 수 있는 작업을 결정하는 프로세스를 말합니다.

인증을 이해하기 위한 또 다른 개념으로 서버, 데이터베이스, 앱, 리소스 등의 공간에 들어가는 것으로 생각할 수 있고, 권한 부여는 사용자가 해당 공간(서버, 데이터베이스 또는 앱) 내에서 어떤 개체에 대해 어떤 작업을 수행할 수 있는지 결정하는 것입니다.

## <a name="common-vulnerabilities-in-software"></a>소프트웨어의 일반적인 취약점

ASP.NET Core 및 EF는 앱을 보호하고 보안 위반을 방지하는 기능을 포함하고 있습니다. 다음 링크 목록을 선택하면 웹앱의 가장 일반적인 보안 취약점을 방지하는 기술을 구체적으로 설명하는 문서로 이동합니다.

* [사이트 간 스크립팅 공격](xref:security/cross-site-scripting)
* [SQL 삽입 공격](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [CSRF(사이트 간 요청 위조)](xref:security/anti-request-forgery)
* [오픈 리디렉션 공격](xref:security/preventing-open-redirects)

그 외에도 알고 계셔야 하는 취약점이 더 있습니다. 자세한 내용은 이 문서의 *ASP.NET Core 보안 설명서*에 대한 섹션을 참조하세요.

## <a name="aspnet-core-security-documentation"></a>ASP.NET Core 보안 설명서

*   [인증](xref:security/authentication/index)
    *   [ID 소개](xref:security/authentication/identity)
    *   [Facebook, Google 및 기타 외부 공급자를 통해 인증 사용](xref:security/authentication/social/index)
    *   [WS-Federation을 사용하여 인증하도록 설정](xref:security/authentication/ws-federation)
    * [Windows 인증 구성](xref:security/authentication/windowsauth)
    *   [계정 확인 및 암호 복구](xref:security/authentication/accconfirm)
    *   [SMS를 사용한 2단계 인증](xref:security/authentication/2fa)
    *   [ID 없이 쿠키 인증 사용](xref:security/authentication/cookie)
    *   [Azure Active Directory](xref:security/authentication/azure-active-directory/index)
        *   [ASP.NET Core 웹앱에 Azure AD 통합](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [Azure AD를 사용하여 WPF 앱에서 ASP.NET Core Web API 호출](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [Azure AD를 사용하여 ASP.NET Core 웹앱에서 Web API 호출](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [Azure AD B2C를 사용하여 ASP.NET Core 웹앱](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [IdentityServer4를 사용하여 ASP.NET Core 앱 보호](https://identityserver4.readthedocs.io)
*   [권한 부여](xref:security/authorization/index)
    *   [소개](xref:security/authorization/introduction)
    *   [권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기](xref:security/authorization/secure-data)
    *   [단순 권한 부여](xref:security/authorization/simple)
    *   [역할 기반 권한 부여](xref:security/authorization/roles)
    *   [클레임 기반 권한 부여](xref:security/authorization/claims)
    *   [정책 기반 권한 부여](xref:security/authorization/policies)
    *   [요구 사항 처리기의 종속성 주입](xref:security/authorization/dependencyinjection)
    *   [리소스 기반 권한 부여](xref:security/authorization/resourcebased)
    *   [보기 기반 권한 부여](xref:security/authorization/views)
    *   [구성표로 ID 제한](xref:security/authorization/limitingidentitybyscheme)
*   [데이터 보호](xref:security/data-protection/index)
    *   [데이터 보호 소개](xref:security/data-protection/introduction)
    *   [데이터 보호 API 시작](xref:security/data-protection/using-data-protection)
    *   [소비자 API](xref:security/data-protection/consumer-apis/index)
        *   [소비자 API 개요](xref:security/data-protection/consumer-apis/overview)
        *   [용도 문자열](xref:security/data-protection/consumer-apis/purpose-strings)
        *   [용도 계층 구조 및 다중 테넌트](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)
        *   [해시 암호](xref:security/data-protection/consumer-apis/password-hashing)
        *   [보호된 페이로드의 수명 제한](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)
        *   [호출된 키가 속한 페이로드 보호 해제](xref:security/data-protection/consumer-apis/dangerous-unprotect)
    *   [구성](xref:security/data-protection/configuration/index)
        *   [데이터 보호 구성](xref:security/data-protection/configuration/overview)
        *   [기본 설정](xref:security/data-protection/configuration/default-settings)
        *   [컴퓨터 수준의 정책](xref:security/data-protection/configuration/machine-wide-policy)
        *   [비 DI 인식 시나리오](xref:security/data-protection/configuration/non-di-scenarios)
    *   [확장성 API](xref:security/data-protection/extensibility/index)
        *   [Core 암호화 확장성](xref:security/data-protection/extensibility/core-crypto)
        *   [키 관리 확장성](xref:security/data-protection/extensibility/key-management)
        *   [기타 API](xref:security/data-protection/extensibility/misc-apis)
    *   [구현](xref:security/data-protection/implementation/index)
        *   [인증된 암호화 세부 정보](xref:security/data-protection/implementation/authenticated-encryption-details)
        *   [하위 키 파생 및 인증된 암호화](xref:security/data-protection/implementation/subkeyderivation)
        *   [컨텍스트 헤더](xref:security/data-protection/implementation/context-headers)
        *   [키 관리](xref:security/data-protection/implementation/key-management)
        *   [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)
        *   [미사용 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest)
        *   [키 불변성 및 설정](xref:security/data-protection/implementation/key-immutability)
        *   [키 저장소 형식](xref:security/data-protection/implementation/key-storage-format)
        *   [삭제되는 데이터 보호 공급자](xref:security/data-protection/implementation/key-storage-ephemeral)
    *   [호환성](xref:security/data-protection/compatibility/index)
        *   [ASP.NET에서 <machineKey> 바꾸기](xref:security/data-protection/compatibility/replacing-machinekey)
*   [권한 부여로 보호된 사용자 데이터를 사용하여 앱 만들기](xref:security/authorization/secure-data)
*   [개발 중인 안전한 앱 비밀 저장소](xref:security/app-secrets)
*   [Azure Key Vault 구성 공급자](xref:security/key-vault-configuration)
*   [SSL 적용](xref:security/enforcing-ssl)
*   [요청 위조 방지](xref:security/anti-request-forgery)
*   [오픈 리디렉션 공격 방지](xref:security/preventing-open-redirects)
*   [사이트 간 스크립팅 방지](xref:security/cross-site-scripting)
*   [원본 간 요청(CORS) 사용](xref:security/cors)
*   [앱 간 쿠키 공유](xref:security/cookie-sharing)
