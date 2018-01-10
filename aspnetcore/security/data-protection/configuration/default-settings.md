---
title: "ASP.NET Core의 데이터 보호 키 관리 및 수명"
author: rick-anderson
description: "ASP.NET Core의 데이터 보호 키 관리 및 수명에 관해서 알아봅니다."
keywords: "ASP.NET Core 키 관리, DPAPI, 데이터 보호 키 수명"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: ef7dad2a-7029-4ae5-8f06-1fbebedccaa4
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: 4f5409acf4d934ced828153ccfd945834d0f1718
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a>ASP.NET Core의 데이터 보호 키 관리 및 수명

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="key-management"></a>키 관리

응용 프로그램은 자신이 실행되는 운영 환경을 감지해서 자체적으로 키 구성을 처리하려고 시도합니다.

1. 응용 프로그램이 [Azure 앱](https://azure.microsoft.com/services/app-service/)에서 호스트될 경우, 키는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다. 이 폴더는 네트워크 저장소에 의해 지원되며 응용 프로그램을 호스팅하는 모든 머신에서 동기화됩니다. 
   * 저장된 비활성 키는 보호되지 않습니다.
   * *DataProtection-Keys* 폴더는 단일 배포 슬롯에 위치한 응용 프로그램의 모든 인스턴스에 키 링을 제공합니다.
   * 스테이징 및 프로덕션, 같은 별도 배포 슬롯 키 링을 공유 하지 않습니다. 예를 들어 스테이징 및 프로덕션을 교체 하거나 A를 사용 하 여 배포 슬롯 간에 교환 / B 테스트, 모든 앱 데이터 보호를 사용 하 여 이전 슬롯 내 키 링을 사용 하 여 저장 된 데이터를 해독할 수 없습니다. 이 데이터 보호를 사용 하 여 쿠키를 보호 하기 위해 표준 ASP.NET Core 쿠키 인증을 사용 하는 응용 프로그램에서 기록 되 고 사용자에 게 이어집니다. 슬롯에 관계 없이 키 링을 원하는 경우 Azure Blob 저장소, Azure 주요 자격 증명 모음 SQL 저장소 등의 외부 키 링 공급자를 사용 하거나 Redis 캐시 합니다. 

1. 사용자 프로필이 사용 가능한 경우에는 *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* 폴더에 키가 저장됩니다. 만약 운영 체제가 Windows라면 저장된 비활성 키가 DPAPI를 통해서 암호화됩니다.

1. 응용 프로그램이 IIS에서 호스트되는 경우에는 작업자 프로세스 계정에만 ACL로 허용된 HKLM 레지스트리 하위의 특수한 레지스트리 키에 키가 저장됩니다. 저장된 비활성 키는 DPAPI를 통해서 암호화됩니다. 

1. 지금까지 살펴본 모든 조건과 일치하지 않으면 현재 프로세스 외부에서는 키가 유지되지 않습니다. 따라서 프로세스가 종료되면 생성된 모든 키가 사라집니다.

Docker 컨테이너에서 호스트되는 경우에는 Docker 볼륨의 폴더 (공유 볼륨이나 호스트 탑재 볼륨같이 컨테이너의 수명과 무관하게 유지되는) 또는 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 및 [Redis](https://redis.io/) 같은 외부 공급자의 폴더에 키를 저장해야 합니다. 이런 외부 공급자는 응용 프로그램이 공유 네트워크 볼륨에 접근할 수 없는 상황의 웹 팜 시나리오에서도 유용합니다 (자세한 내용은 [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem)을 참고하시기 바랍니다). 

Docker 컨테이너에서 호스트 되는 경우에는  Docker 볼륨의 폴더 (공유 볼륨이나 호스트 탑재 볼륨 같이 컨테이너의 수명과 무관하게 유지되는) 또는 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 및 [Redis](https://redis.io/) 같은 외부 공급자의 폴더에 키를 저장해야 합니다. 이런 외부 공급자는 응용 프로그램이 공유 네트워크 볼륨에 접근할 수 없는 상황의 웹 팜 시나리오에서도 유용합니다 (자세한 내용은 [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem)을 참고하시기 바랍니다).

> [!WARNING]
> 개발자가 기본 구성을 재정의해서 데이터 보호 시스템이 특정 키 저장소를 바라보도록 지정하면, 저장된 비활성 키의 자동 암호화가 비활성화됩니다. 저장된 비활성 키의 보호 기능은 [구성](xref:security/data-protection/configuration/overview)을 통해서 다시 활성화시킬 수 있습니다.

## <a name="key-lifetime"></a>키 수명

기본으로 사용되는 페이로드 보호 알고리즘은 기밀성을 위한 AES-256-CBC와 신뢰성을 위한 HMACSHA256입니다. 페이로드 별로 매 90일마다 롤링되는 512비트 마스터 키를 사용해서 이 알고리즘들에 사용되는 두 개의 하위 키가 파생됩니다. 더 자세한 정보는 [하위 키 파생](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation)을 참고하시기 바랍니다.

## <a name="default-algorithms"></a>기본 알고리즘

기본으로 사용되는 페이로드 보호 알고리즘은 기밀성을 위한 AES-256-CBC와 신뢰성을 위한 HMACSHA256입니다. 페이로드 별로 매 90일 마다 롤링되는 512 비트 마스터 키를 사용해서 이 알고리즘들에 사용되는 두 개의 하위 키가 파생됩니다. 더 자세한 정보는 [하위 키 파생](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation)을 참고하시기 바랍니다.

## <a name="see-also"></a>참고 항목

* [키 관리 확장성](xref:security/data-protection/extensibility/key-management)
