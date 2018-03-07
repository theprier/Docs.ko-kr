---
title: "ASP.NET Core의 데이터 보호 키 관리 및 수명"
author: rick-anderson
description: "ASP.NET Core의 데이터 보호 키 관리 및 수명에 관해서 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: b43c14af015d5e03f46200c51a1218a581b1de0c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a>ASP.NET Core의 데이터 보호 키 관리 및 수명

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="key-management"></a>키 관리

응용 프로그램은 자신이 실행되는 운영 환경을 감지해서 자체적으로 키 구성을 처리하려고 시도합니다.

1. 응용 프로그램에서 호스트 될 경우 [Azure 앱](https://azure.microsoft.com/services/app-service/), 키에 저장 됩니다는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더입니다. 이 폴더는 네트워크 저장소에서 지원 하 고 응용 프로그램을 호스트 하는 모든 컴퓨터에서 동기화 됩니다.
   * 저장된 비활성 키는 보호되지 않습니다.
   * *DataProtection-Keys* 폴더는 단일 배포 슬롯에 위치한 응용 프로그램의 모든 인스턴스에 키 링을 제공합니다.
   * 스테이징 및 프로덕션, 같은 별도 배포 슬롯 키 링을 공유 하지 않습니다. 예를 들어 스테이징 및 프로덕션을 교체 하거나 A를 사용 하 여 배포 슬롯 간에 교환 / B 테스트, 모든 앱 데이터 보호를 사용 하 여 이전 슬롯 내 키 링을 사용 하 여 저장 된 데이터를 해독할 수 없습니다. 이 데이터 보호를 사용 하 여 쿠키를 보호 하기 위해 표준 ASP.NET Core 쿠키 인증을 사용 하는 응용 프로그램에서 기록 되 고 사용자에 게 이어집니다. 슬롯에 관계 없이 키 링을 원하는 경우 Azure Blob 저장소, Azure 주요 자격 증명 모음 SQL 저장소 등의 외부 키 링 공급자를 사용 하거나 Redis 캐시 합니다.

1. 사용자 프로필이 사용 가능한 경우에는 *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* 폴더에 키가 저장됩니다. 운영 체제가 Windows 인 경우 키 DPAPI를 사용 하 여 암호화 됩니다.

1. 응용 프로그램이 IIS에서 호스트되는 경우에는 작업자 프로세스 계정에만 ACL로 허용된 HKLM 레지스트리 하위의 특수한 레지스트리 키에 키가 저장됩니다. 저장된 비활성 키는 DPAPI를 통해서 암호화됩니다.

1. 지금까지 살펴본 모든 조건과 일치하지 않으면 현재 프로세스 외부에서는 키가 유지되지 않습니다. 따라서 프로세스가 종료되면 생성된 모든 키가 사라집니다.

개발자는 언제나 모든 제어 권한을 갖고 있으며 키가 저장되는 방식과 위치를 재정의할 수 있습니다. 위의 옵션 중, 처음 세 옵션은 기존에 ASP.NET  **\<machineKey >** 자동 생성 루틴이 동작하던 방식과 유사하며 대부분의 응용 프로그램에 적합한 기본 구성입니다. 유일하게 마지막 대체 옵션만 키 지속성을 원할 경우 개발자가 사전 [구성](xref:security/data-protection/configuration/overview) 작업을 수행해야 하는 시나리오지만, 이런 대체 시나리오는 매우 드물게 발생합니다.

Docker 볼륨 (공유 볼륨 또는 컨테이너의 수명이 지속 되 면 호스트 탑재 된 볼륨)가 있는 폴더에 키를 유지할지를 Docker 컨테이너에서 호스팅하는 경우 또는 외부 공급자와 같은 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)합니다. 앱 공유 네트워크 볼륨에 액세스할 수 없는 경우 외부 공급자 웹 팜 시나리오에 도움이 됩니다 (참조 [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) 자세한 정보에 대 한).

> [!WARNING]
> 개발자가 기본 구성을 재정의해서 데이터 보호 시스템이 특정 키 저장소를 바라보도록 지정하면, 저장된 비활성 키의 자동 암호화가 비활성화됩니다. 저장된 비활성 키의 보호 기능은 [구성](xref:security/data-protection/configuration/overview)을 통해서 다시 활성화시킬 수 있습니다.

## <a name="key-lifetime"></a>키 수명

키는은 기본적으로는 90 일 수명을 갖습니다. 키 만료 되 면 응용 프로그램 자동으로 새 키를 생성 하 고 새 키를 활성 키로 설정 합니다. 사용 중지 된 키를 시스템에 유지,으로 앱 사람과 보호 되는 모든 데이터를 해독할 수 있습니다. 참조 [키 관리](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) 자세한 정보에 대 한 합니다.

## <a name="default-algorithms"></a>기본 알고리즘

기본 페이로드 보호 알고리즘 사용은 AES-256-CBC 기밀성 및 HMACSHA256에 대 한 신뢰성에 대 한 합니다. 페이로드 당 별로 이러한 알고리즘에 사용 되는 두 개의 하위 키를 파생 90 일 마다 변경 512 비트 마스터 키가 사용 됩니다. 참조 [파생 하위](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) 자세한 정보에 대 한 합니다.

## <a name="see-also"></a>참고 항목

* [키 관리 확장성](xref:security/data-protection/extensibility/key-management)
