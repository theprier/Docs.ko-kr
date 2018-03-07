---
title: "데이터 보호 소개"
author: rick-anderson
description: "이 문서는 데이터 보호의 개념을 소개하고 관련된 ASP.NET Core API의 디자인 원칙을 간략하게 설명합니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/introduction
ms.openlocfilehash: acd38679390b92705703111b72816f1a5d3ba848
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-data-protection"></a>데이터 보호 소개

웹 응용 프로그램은 종종 보안이 중요 한 데이터를 저장 해야 합니다. Windows 데스크톱 응용 프로그램에 대 한 DPAPI를 제공 하지만 웹 응용 프로그램에 적합 하지 않습니다. ASP.NET Core 데이터 보호 스택의 개발자 키 관리 및 회전을 포함 한 데이터를 보호 사용할 수 있는 간단 하 고 사용 하기 쉬운 암호화 API를 제공 합니다.

ASP.NET Core 데이터 보호 스택은 장기적으로 ASP.NET 1.x - 4.x의 요소를 대체하기 위한 목적으로 설계되었습니다. 기존 암호화 스택의 많은 단점을 해결하는 한편, 현대적인 응용 프로그램에서 접할 수 있는 대부분의 사용 사례에 즉각적으로 대응할 수 있는 솔루션을 제공하도록 설계되었습니다.

## <a name="problem-statement"></a>문제 설명

전체적인 문제를 다음 한 문장으로 간단 명료하게 정리할 수 있습니다: 나중에 검색에 대 한 신뢰할 수 있는 정보를 유지 해야 하지만 지 속성 메커니즘이 신뢰 하지 않습니다. 웹의 관점에서 다시 말하자면 "신뢰할 수 있는 상태를 신뢰할 수 없는 클라이언트를 통해서 왕복해야(Round-Trip) 한다"고 할 수 있습니다."

대표적인 사례가 인증 쿠키나 전달자 토큰(Bearer Token)의 경우입니다. 서버가 "나는 Groot고 xyz 권한을 갖고 있다"라는 토큰을 생성해서 클라이언트로 전달합니다. 이후 특정 시점에 클라이언트가 다시 서버로 해당 토큰을 제출하지만 서버로서는 클라이언트가 해당 토큰을 변조하지 않았다는 어떤한 보장이 필요합니다. 따라서 필요한 첫 번째 요건은 신뢰성(Authenticity)입니다(무결성(Integrity) 또는 변조 방지(Tamper-Proofing)하고도 합니다).

그리고 저장된 상태(정보)를 신뢰하는 주체는 서버이므로, 이 상태에 운영 환경 고유의 정보가 포함되어 있을 수도 있음을 예상할 수 있습니다. 이 정보는 파일 경로, 권한, 핸들 혹은 그 밖의 간접 참조, 또는 서버 고유의 데이터 중 일부 같은 형태를 갖출 수도 있습니다. 일반적으로 이런 정보들은 신뢰할 수 없는 클라이언트에게는 공개되지 않습니다. 따라서 필요한 두 번째 요건은 기밀성(Confidentiality)입니다.

마지막으로 현대적 응용 프로그램은 구성 요소를 기반으로 구축되므로 각 개별 구성 요소는 시스템의 다른 구성 요소들과 관계없이 이 시스템(데이터 보호 스택)을 활용할 수 있어야 합니다. 예를 들어, 전달자 토큰 구성 요소가 데이터 보호 스택을 사용한다면 역시 같은 스택을 사용하는 CSRF 방지 메커니즘의 간섭없이 동작할 수 있어야 합니다. 따라서 필요한 마지막 요건은 격리(Isolation)입니다.

더 많은 제약 조건을 규정해서 필요 요건의 범위를 좁힐 수 있습니다. 암호화 시스템 내에서 작동 하는 모든 서비스는 동일 하 게 신뢰할 수 있도록 하 고 데이터를 생성 하거나 우리의 직접 제어를 받는 서비스 외부에서 사용 된 필요 하지 않습니다 가정 합니다. 또한, 웹 서비스에 대한 각 요청이 암호화 시스템을 여러 번 거칠 수도 있기 때문에 최대한 빠르게 작업을 처리해야 합니다. 이로써 대칭 암호화 시나리오에 대 한 이상적인 며 등 필요한에 한 번까지 비대칭 암호화 할인 수 있습니다.

## <a name="design-philosophy"></a>디자인 원칙

먼저 우리는 기존 스택과 관련된 문제점을 확인하는 작업에 착수했습니다. 이 작업을 마치고 기존 솔루션의 현황을 조사해본 결과, 기존 솔루션에는 원하는 기능들이 전혀 존재하지 않는다는 결론을 내렸습니다. 이후, 다음과 같은 몇 가지 기본 원칙에 따라 솔루션을 설계했습니다.

* 시스템 구성 방식이 간단해야 합니다. 이상적으로는 특별히 시스템을 구성하지 않고도(Zero-Configuration) 개발자들이 작업하는 데 전혀 지장이 없어야 합니다. 개발자가 특정 측면(예: 키 저장소)을 구성해야 할 경우, 해당 특정 구성을 간단히 처리할 수 있는 방법이 제공되어야 합니다.

* 간단한 소비자 지향적인 API를 제공해야 합니다. 이 API는 올바르게 사용하기는 쉽고 잘못 사용하기는 어려워야 합니다.

* 개발자는 키 관리 원칙 배울 하지 않아야 합니다. 알고리즘 선택 및 개발자의를 대신 하 여 키 수명 시스템이 처리 해야 합니다. 이상적으로 개발자 원시 키 자료에 액세스를 권한이 하지 않습니다.

* 가능 하면 저장 된 상태의 키를 보호 해야 합니다. 시스템에서는 적절 한 기본 보호 메커니즘을 파악 하 고 자동으로 적용 해야 합니다.

이러한 원칙을 염두 우리는 간단한 개발 [사용 하기 쉬운](using-data-protection.md) 데이터 보호 스택의 합니다.

ASP.NET Core 데이터 보호 Api는 주로 없습니다 기밀 페이로드의 무한 지 속성. 와 같은 다른 기술은 [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) 및 [Azure 권한 관리](https://docs.microsoft.com/rights-management/) 무한 저장소 시나리오에 보다 적합 한까지 강력한 키 관리 기능을 갖습니다. 즉, 개발자는 ASP.NET Core 데이터 보호 Api를 사용 하 여 기밀 데이터의 장기 보호에 대 한 일은 없습니다.

## <a name="audience"></a>대상 사용자

데이터 보호 시스템 주 다섯 개의 패키지로으로 구분 됩니다. 이러한 Api의 다양 한 측면에는 세 가지 주요 대상; 대상

1. [소비자 Api 개요](consumer-apis/overview.md) 대상 프레임 워크 및 응용 프로그램 개발자.

   "싶지 스택 작동 하는 방법에 대 한 또는 구성 된 방식에 대 한 자세한 내용을 알아보려면 합니다. 단순히 하겠습니다 일부로 작업을 수행에 단순한 방식으로 가능한 Api를 사용 하 여 성공적으로 확률이 높은. "

2. [구성 Api](configuration/overview.md) 응용 프로그램 개발자 및 시스템 관리자가 대상으로 합니다.

   "기본이 아닌 경로 또는 설정 내 환경 필요 함을 데이터 보호 시스템에 알려 하고자 합니다."

3. 확장성 개발자는 Api 대상 사용자 지정 정책을 구현 하는 일을 담당 합니다. 이러한 Api에 드문 경우로 제한 되 고 개발자가 인식 하는 보안을 발생 합니다.

   "하고자 실제로 고유 동작 요구 사항을 때문에 시스템 내에서 전체 구성 요소를 대체 합니다. 하겠습니다 내 요구 사항을 충족 하는 플러그 인을 작성 하기 위해 API 화면의 프로토콜과 사용 하지 않는 부분에 알아보려면. "

## <a name="package-layout"></a>패키지 레이아웃

데이터 보호 스택의 다섯 개의 패키지로 구성 됩니다.

* Microsoft.AspNetCore.DataProtection.Abstractions 기본 IDataProtectionProvider 및 IDataProtector 인터페이스를 포함합니다. 또한 이러한 형식 (예: 오버 로드의 IDataProtector.Protect) 작업을 지원할 수 있는 유용한 확장 메서드를 포함 합니다. 자세한 내용은 소비자 인터페이스 단원을 참조 하십시오. 다른 사람에 게는 데이터 보호 시스템 인스턴스화를 담당 하는 경우 단순히 Api를 사용 하는 Microsoft.AspNetCore.DataProtection.Abstractions 참조 합니다.

* Microsoft.AspNetCore.DataProtection 핵심 암호화 작업, 키 관리, 구성 및 확장성을 포함 하 여 데이터 보호 시스템의 핵심 구현을 포함 합니다. 데이터 보호 시스템 인스턴스화를 담당 하는 경우 (예:에 추가 IServiceCollection)를 수정 하거나 해당 동작을 확장 해야 Microsoft.AspNetCore.DataProtection 참조 또는 합니다.

* Microsoft.AspNetCore.DataProtection.Extensions는 개발자가 유용할 수 있지만 코어 패키지에 속해 있지 않습니다는 추가 Api를 포함 합니다. 예를 들어,이 패키지는 간단한 "종속성 주입 설치 하지 않고도 특정 키 저장소 디렉터리를 가리키는 시스템 인스턴스화할" API (추가 정보)를 포함합니다. 또한 보호 된 페이로드 (추가 정보)의 수명을 제한 하기 위한 확장 메서드를 포함 합니다.

* Microsoft.AspNetCore.DataProtection.SystemWeb 패키지를 기존의 ASP.NET 4.x 응용 프로그램에 설치하면 그 내부의 <machineKey> 처리 대신 새로운 데이터 보호 스택을 사용하도록 재지정할 수 있습니다. 보다 자세한 정보는 [호환성](compatibility/replacing-machinekey.md#compatibility-replacing-machinekey) 을 참고하시기 바랍니다.

* Microsoft.AspNetCore.Cryptography.KeyDerivation 루틴 해시 PBKDF2 암호의 구현을 제공 하 고 사용자 암호를 안전 하 게 처리 하는 데 필요한 시스템에서 사용 될 수 있습니다. 참조 [암호 해시](consumer-apis/password-hashing.md) 자세한 정보에 대 한 합니다.
