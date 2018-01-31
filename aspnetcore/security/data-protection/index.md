---
title: "ASP.NET Core에서 데이터 보호"
author: rick-anderson
description: "이 문서는 다양한 ASP.NET Core 데이터 보호 항목에 대한 목차로 사용됩니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/index
ms.openlocfilehash: b846fb7cb28eeceb8c0bdb47135e1cf014ae08a7
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a>ASP.NET Core에서 데이터 보호: 소비자 API, 구성, 확장성 API 및 구현

* [데이터 보호 소개](introduction.md)

* [데이터 보호 API 시작](using-data-protection.md)

* [소비자 API](consumer-apis/index.md)

  * [소비자 API 개요](consumer-apis/overview.md)

  * [용도 문자열](consumer-apis/purpose-strings.md)

  * [용도 계층 구조 및 다중 테넌트](consumer-apis/purpose-strings-multitenancy.md)

  * [암호 해시](consumer-apis/password-hashing.md)

  * [보호된 페이로드의 수명 제한](consumer-apis/limited-lifetime-payloads.md)

  * [호출된 키가 속한 페이로드 보호 해제](consumer-apis/dangerous-unprotect.md)

* [구성](configuration/index.md)

  * [데이터 보호 구성](configuration/overview.md)

  * [기본 설정](configuration/default-settings.md)

  * [컴퓨터 수준의 정책](configuration/machine-wide-policy.md)

  * [비 DI 인식 시나리오](configuration/non-di-scenarios.md)

* [확장성 API](extensibility/index.md)

  * [Core 암호화 확장성](extensibility/core-crypto.md)

  * [키 관리 확장성](extensibility/key-management.md)

  * [기타 API](extensibility/misc-apis.md)

* [구현](implementation/index.md)

  * [인증된 암호화 세부 정보](implementation/authenticated-encryption-details.md)

  * [하위 키 파생 및 인증된 암호화](implementation/subkeyderivation.md)

  * [컨텍스트 헤더](implementation/context-headers.md)

  * [키 관리](implementation/key-management.md)

  * [키 저장소 공급자](implementation/key-storage-providers.md)

  * [미사용 키 암호화](implementation/key-encryption-at-rest.md)

  * [키 불변성 및 설정 변경](implementation/key-immutability.md)

  * [키 저장소 형식](implementation/key-storage-format.md)

  * [삭제되는 데이터 보호 공급자](implementation/key-storage-ephemeral.md)

* [호환성](compatibility/index.md)

  * [앱 간 쿠키 공유](xref:security/data-protection/compatibility/cookie-sharing)

  * [ASP.NET에서 <machineKey> 바꾸기](xref:security/data-protection/compatibility/replacing-machinekey)
