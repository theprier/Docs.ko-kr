---
title: ASP.NET Core의 불변성 및 키 설정 키
author: rick-anderson
description: ASP.NET Core 데이터 보호 키 불변성 Api의 구현 세부 정보에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-immutability
ms.openlocfilehash: 45460e0bdf6ad0a978f984d55b64f562c13fb575
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36279456"
---
# <a name="key-immutability-and-key-settings-in-aspnet-core"></a>ASP.NET Core의 불변성 및 키 설정 키

개체는 백업 저장소에 유지 되 면 표현 영원히 고정 되어 있습니다. 새 데이터에는 백업 저장소에 추가할 수 있지만 기존 데이터를 변경할 수 없습니다. 이 동작의 주 목적은 데이터 손상을 방지 하려면입니다.

이 동작의 한 결과 키를 백업 저장소에 쓴 후 아닌지 변경할 수는입니다. 생성, 활성화 및 만료 날짜는 변경할 수 없습니다, 사용 하 여 취소할 수 있지만 `IKeyManager`합니다. 또한 해당 기본 알고리즘 정보, 마스터 키 자료 및 나머지 속성에서 암호화도 변경할 수 없는 합니다.

다음에 키를 생성 하기 위해 명시적 호출이 통해 될 때까지 해당 변경 내용이 반영 다루지는 않겠습니다. 개발자는 설정 키 지 속성에 영향을 주는 변경 되 면 `IKeyManager.CreateNewKey` 또는 데이터 보호 시스템의 자체를 통해 [자동 키 세대](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) 동작 합니다. 지 속성 키에 영향을 주는 설정은 다음과 같습니다.

* [기본 키 수명](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)

* [나머지 메커니즘에 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest)

* [키 내에 포함 된 알고리즘 정보](xref:security/data-protection/configuration/overview#changing-algorithms-with-usecryptographicalgorithms)

이러한 설정은 다음 자동 키 롤링 시간 이전의 조정이 시작 해야 할 경우 만드는 것을 고려 하기 위해 명시적 호출이 `IKeyManager.CreateNewKey` 를 새 키를 만들어야 합니다. 명시적으로 활성화 날짜를 제공 해야 합니다. ({이제 + 2 일을 (를)이는 바람직한 방법은 전파에 대 한 변경에 대 한 시간을 허용 하도록) 및 호출에 대 한 만료 날짜입니다.

>[!TIP]
> 저장소를 변경 하는 모든 응용 프로그램에 사용 하 여 동일한 설정을 지정 해야는 `IDataProtectionBuilder` 확장 메서드입니다. 그렇지 않으면, 지속형된 키의 속성 키 생성 루틴을 호출 하는 특정 응용 프로그램에 종속 됩니다.
