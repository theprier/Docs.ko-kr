---
title: "데이터 보호 시스템 수준의 정책에서 ASP.NET Core 지원"
author: rick-anderson
description: "ASP.NET Core 데이터 보호를 사용 하는 모든 앱에 대 한 기본 시스템 수준의 정책 설정에 대 한 지원에 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/machine-wide-policy
ms.openlocfilehash: 4c3ae3b628ebe17c7926c71f1fad664d719d1706
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="data-protection-machine-wide-policy-support-in-aspnet-core"></a>데이터 보호 시스템 수준의 정책에서 ASP.NET Core 지원

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

Windows에서 실행 하는 경우 데이터 보호 시스템 ASP.NET Core 데이터 보호를 사용 하는 모든 앱에 대 한 기본 시스템 수준의 정책 설정에 대 한 지원이 제한 합니다. 일반적인 개념은 관리자가 사용 된 알고리즘 같은 기본값을 설정 하거나 수동으로 컴퓨터에 모든 응용 프로그램을 업데이트 하지 않아도 키 수명을 변경 수 있습니다.

> [!WARNING]
> 시스템 관리자는 기본 정책을 설정할 수 있지만 이러한 적용할 수 없습니다. 앱 개발자 자신의 선택 중 하나가 지정 된 모든 값을 무시할 수 있습니다. 기본 정책 응용 프로그램을 개발자는 설정에 대 한 명시적 값을 지정 하지 않은 위치에 영향을 줍니다.

## <a name="setting-default-policy"></a>기본 정책 설정

기본 정책을 설정 하려면 관리자가 다음 레지스트리 키 아래 시스템 레지스트리에 알려진된 값을 설정할 수 있습니다.

**HKLM\SOFTWARE\Microsoft\DotNetPackages\Microsoft.AspNetCore.DataProtection**

64 비트 운영 체제에 32 비트 응용 프로그램의 동작에 영향을 하려는 하는 경우 위의 키에 해당 하는 Wow6432Node 구성 해야 합니다.

지원 되는 값은 다음과 같습니다.

| 값              | 형식   | 설명 |
| ------------------ | :----: | ----------- |
| EncryptionType     | string | 데이터 보호에 사용할 알고리즘을 지정 합니다. 값은 CNG CBC, CNG-GCM 또는 관리 되는 이어야 하며 아래에서 자세히 설명 합니다. |
| DefaultKeyLifetime | DWORD  | 새로 생성 된 키에 대 한 수명을 지정합니다. 값 일 단위로 지정 하 고 있어야 > = 7 까지의 유형은 합니다. |
| KeyEscrowSinks     | string | 키 위탁 사용 되는 형식을 지정 합니다. 값은 키 에스크로 싱크, 여기서 목록의 각 요소는 구현 하는 형식의 어셈블리 정규화 된 이름을 세미콜론으로 구분 된 목록 [IKeyEscrowSink](/dotnet/api/microsoft.aspnetcore.dataprotection.keymanagement.ikeyescrowsink)합니다. |

## <a name="encryption-types"></a>암호화 종류

암호를 사용 하는 CBC 모드 대칭 블록 기밀성 및 HMAC에 대 한 신뢰성에 대 한 Windows CNG에서 제공 하는 서비스와 시스템이 구성 EncryptionType CNG CBC 이면 (참조 [사용자 지정 Windows CNG 알고리즘을 지정 하](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) 에 대 한 자세한 내용은) 있습니다. 다음 추가 값은 지원, 있으며 각각 CngCbcAuthenticatedEncryptionSettings 형식의 속성에 해당 합니다.

| 값                       | 형식   | 설명 |
| --------------------------- | :----: | ----------- |
| EncryptionAlgorithm         | string | CNG에서 인식 하는 대칭 블록 암호화 알고리즘의 이름입니다. 이 알고리즘 CBC 모드에서 열립니다. |
| EncryptionAlgorithmProvider | string | EncryptionAlgorithm 알고리즘을 만들 수 있는 구현 CNG 공급자의 이름입니다. |
| EncryptionAlgorithmKeySize  | DWORD  | 길이 (비트)를 대칭 블록 암호화 알고리즘에 대 한 파생 키의입니다. |
| HashAlgorithm               | string | CNG에서 인식 하는 해시 알고리즘의 이름입니다. 이 알고리즘 HMAC 모드에서 열립니다. |
| HashAlgorithmProvider       | string | 알고리즘 HashAlgorithm을 만들 수 있는 구현 CNG 공급자의 이름입니다. |

EncryptionType이 CNG GCM, 시스템은 Windows CNG에서 제공 하는 서비스와 기밀성 및 인증에 대 한 Galois/카운터 모드 대칭 블록 암호화를 사용 하도록 구성 (참조 [사용자 지정 Windows CNG 알고리즘을 지정 하](xref:security/data-protection/configuration/overview#specifying-custom-windows-cng-algorithms) 자세한 내용은). 다음 추가 값은 지원, 있으며 각각 CngGcmAuthenticatedEncryptionSettings 형식의 속성에 해당 합니다.

| 값                       | 형식   | 설명 |
| --------------------------- | :----: | ----------- |
| EncryptionAlgorithm         | string | CNG에서 인식 하는 대칭 블록 암호화 알고리즘의 이름입니다. 이 알고리즘 Galois/카운터 모드에서 열립니다. |
| EncryptionAlgorithmProvider | string | EncryptionAlgorithm 알고리즘을 만들 수 있는 구현 CNG 공급자의 이름입니다. |
| EncryptionAlgorithmKeySize  | DWORD  | 길이 (비트)를 대칭 블록 암호화 알고리즘에 대 한 파생 키의입니다. |

시스템이 정품에 대 한 기밀성 및 KeyedHashAlgorithm에 대 한 관리 되는 SymmetricAlgorithm를 사용 하도록 구성 된 EncryptionType 관리 되는 경우 (참조 [지정 하면 사용자 지정 관리 알고리즘](xref:security/data-protection/configuration/overview#specifying-custom-managed-algorithms) 자세한 세부 정보에 대 한). 다음 추가 값은 지원, 있으며 각각 ManagedAuthenticatedEncryptionSettings 형식의 속성에 해당 합니다.

| 값                      | 형식   | 설명 |
| -------------------------- | :----: | ----------- |
| EncryptionAlgorithmType    | string | SymmetricAlgorithm를 구현 하는 형식의 어셈블리 정규화 된 이름입니다. |
| EncryptionAlgorithmKeySize | DWORD  | 길이 (비트)를 대칭 암호화 알고리즘에 대 한 파생 키의입니다. |
| ValidationAlgorithmType    | string | KeyedHashAlgorithm을 구현 하는 형식의 어셈블리 정규화 된 이름입니다. |

EncryptionType 빈 또는 null이 아닌 다른 값이 있으면 데이터 보호 시스템 시작 시 예외를 throw 합니다.

> [!WARNING]
> 형식 이름 (EncryptionAlgorithmType, ValidationAlgorithmType, KeyEscrowSinks)를 포함 하는 기본 정책 설정을 구성할 때 형식을 응용 프로그램에 제공 해야 합니다. 이 응용 프로그램의 데스크톱 CLR에서 실행 중인 경우 이러한 형식을 포함 하는 어셈블리 해야 함을 전역 어셈블리 캐시 (GAC)에 있는 것을 의미 합니다. 실행 중인 ASP.NET Core 응용 프로그램에 대 한 [.NET Core](https://www.microsoft.com/net/core), 이러한 형식을 포함 하는 패키지를 설치 해야 합니다.
