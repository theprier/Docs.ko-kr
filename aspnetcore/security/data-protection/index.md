---
title: ASP.NET Core에서 데이터 보호
author: rick-anderson
description: 이 문서는 다양한 ASP.NET Core 데이터 보호 항목에 대한 목차로 사용됩니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/index
ms.openlocfilehash: 1c38c587956dd99078fa4386c2f4423d784abc60
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277126"
---
# <a name="data-protection-in-aspnet-core"></a>ASP.NET Core에서 데이터 보호

* [데이터 보호 소개](xref:security/data-protection/introduction)

* [데이터 보호 API 시작](xref:security/data-protection/using-data-protection)

* [소비자 API](xref:security/data-protection/consumer-apis/index)

  * [소비자 API 개요](xref:security/data-protection/consumer-apis/overview)

  * [용도 문자열](xref:security/data-protection/consumer-apis/purpose-strings)

  * [용도 계층 구조 및 다중 테넌트](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [해시 암호](xref:security/data-protection/consumer-apis/password-hashing)

  * [보호된 페이로드의 수명 제한](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [호출된 키가 속한 페이로드 보호 해제](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [구성](xref:security/data-protection/configuration/index)

  * [ASP.NET Core 데이터 보호 구성](xref:security/data-protection/configuration/overview)

  * [기본 설정](xref:security/data-protection/configuration/default-settings)

  * [컴퓨터 수준의 정책](xref:security/data-protection/configuration/machine-wide-policy)

  * [비 DI 인식 시나리오](xref:security/data-protection/configuration/non-di-scenarios)

* [확장성 API](xref:security/data-protection/extensibility/index)

  * [Core 암호화 확장성](xref:security/data-protection/extensibility/core-crypto)

  * [키 관리 확장성](xref:security/data-protection/extensibility/key-management)

  * [기타 API](xref:security/data-protection/extensibility/misc-apis)

* [구현](xref:security/data-protection/implementation/index)

  * [인증된 암호화 세부 정보](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [하위 키 파생 및 인증된 암호화](xref:security/data-protection/implementation/subkeyderivation)

  * [컨텍스트 헤더](xref:security/data-protection/implementation/context-headers)

  * [키 관리](xref:security/data-protection/implementation/key-management)

  * [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)

  * [미사용 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [키 불변성 및 설정](xref:security/data-protection/implementation/key-immutability)

  * [키 저장소 형식](xref:security/data-protection/implementation/key-storage-format)

  * [삭제되는 데이터 보호 공급자](xref:security/data-protection/implementation/key-storage-ephemeral)

* [호환성](xref:security/data-protection/compatibility/index)

  * [ASP.NET Core에서 ASP.NET <machineKey> 교체](xref:security/data-protection/compatibility/replacing-machinekey)
