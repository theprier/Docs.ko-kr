---
title: "데이터 보호에 대 한 키 관리 및 ASP.NET Core 수명"
author: rick-anderson
description: "데이터 보호 키 관리 및 ASP.NET 코어의 수명에 알아봅니다."
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
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a>데이터 보호에 대 한 키 관리 및 ASP.NET Core 수명

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="key-management"></a>키 관리

응용 프로그램 운영 환경을 검색 하 고 자체적으로 키 구성 처리 하려고 합니다.

1. 응용 프로그램에서 호스트 될 경우 [Azure 앱](https://azure.microsoft.com/services/app-service/), 키에 저장 됩니다는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더입니다. 이 폴더는 네트워크 저장소에서 지원 하 고 응용 프로그램을 호스트 하는 모든 컴퓨터에서 동기화 됩니다.
   * 저장 된 상태의 키를 보호 되지 않습니다.
   * *DataProtection 키* 폴더 키 링을 단일 배포 슬롯에서 응용 프로그램의 모든 인스턴스를 제공 합니다.
   * 스테이징 및 프로덕션, 같은 별도 배포 슬롯 키 링을 공유 하지 않습니다. 예를 들어 스테이징 및 프로덕션을 교체 하거나 A를 사용 하 여 배포 슬롯 간에 교환 / B 테스트, 모든 앱 데이터 보호를 사용 하 여 이전 슬롯 내 키 링을 사용 하 여 저장 된 데이터를 해독할 수 없습니다. 이 데이터 보호를 사용 하 여 쿠키를 보호 하기 위해 표준 ASP.NET Core 쿠키 인증을 사용 하는 응용 프로그램에서 기록 되 고 사용자에 게 이어집니다. 슬롯에 관계 없이 키 링을 원하는 경우 Azure Blob 저장소, Azure 주요 자격 증명 모음 SQL 저장소 등의 외부 키 링 공급자를 사용 하거나 Redis 캐시 합니다.

1. 키에 유지 되기 사용자 프로필을 사용할 수 있는 경우는 *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* 폴더입니다. 운영 체제가 Windows 인 경우 키 DPAPI를 사용 하 여 암호화 됩니다.

1. 응용 프로그램을 IIS에서 호스트 하는 경우 키 하 게 포함 되었는지 작업자 프로세스 계정에만 있는 특별 한 레지스트리 키에서 HKLM 레지스트리 에서도 유지 됩니다. 미사용 키는 DPAPI를 사용하여 암호화됩니다.

1. 일치 이러한 조건 중 없을 경우 현재 프로세스 외부에서 키 유지 되지 않습니다. 생성 된 모든 종료 프로세스가 종료 키 손실 됩니다.

개발자는 항상 모든 권한 및 키가 저장 하는 방법과 재정의할 수 있습니다. 위의 처음 세 옵션은 대부분의 응용 프로그램 방법과 유사 좋은 기본값을 제공 해야 ASP.NET  **\<machineKey >** 자동 생성 루틴 이전에 작동 합니다. 최종, 대체 옵션은 개발자가 지정할 수 필요로 하는 유일한 시나리오 [구성](xref:security/data-protection/configuration/overview) 선행 키 지 속성을 원하는 하지만이 대체 (fallback이) 드문 경우에만 발생 합니다.

Docker 볼륨 (공유 볼륨 또는 컨테이너의 수명이 지속 되 면 호스트 탑재 된 볼륨)가 있는 폴더에 키를 유지할지를 Docker 컨테이너에서 호스팅하는 경우 또는 외부 공급자와 같은 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)합니다. 앱 공유 네트워크 볼륨에 액세스할 수 없는 경우 외부 공급자 웹 팜 시나리오에 도움이 됩니다 (참조 [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) 자세한 정보에 대 한).

> [!WARNING]
> 개발자는 위에 설명 된 규칙을 재정의 하 고 데이터 보호 시스템에 특정 키 저장소를 가리키는, 미사용 키의 자동 암호화는 비활성화 됩니다. Rest에 보호를 통해 다시 사용 되도록 설정 될 수 있습니다 [구성](xref:security/data-protection/configuration/overview)합니다.

## <a name="key-lifetime"></a>키 수명

키는은 기본적으로는 90 일 수명을 갖습니다. 키 만료 되 면 응용 프로그램 자동으로 새 키를 생성 하 고 새 키를 활성 키로 설정 합니다. 사용 중지 된 키를 시스템에 유지,으로 앱 사람과 보호 되는 모든 데이터를 해독할 수 있습니다. 참조 [키 관리](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) 자세한 정보에 대 한 합니다.

## <a name="default-algorithms"></a>기본 알고리즘

기본 페이로드 보호 알고리즘 사용은 AES-256-CBC 기밀성 및 HMACSHA256에 대 한 신뢰성에 대 한 합니다. 페이로드 당 별로 이러한 알고리즘에 사용 되는 두 개의 하위 키를 파생 90 일 마다 변경 512 비트 마스터 키가 사용 됩니다. 참조 [파생 하위](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) 자세한 정보에 대 한 합니다.

## <a name="see-also"></a>참고 항목

* [키 관리 확장성](xref:security/data-protection/extensibility/key-management)
