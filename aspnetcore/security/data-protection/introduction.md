---
title: ASP.NET Core 데이터 보호
author: rick-anderson
description: 데이터 보호의 개념 및 ASP.NET Core 데이터 보호 Api의 디자인 원칙에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/introduction
ms.openlocfilehash: 5526b517ba9f1ac4b041576156b2964217460726
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="aspnet-core-data-protection"></a>ASP.NET Core 데이터 보호

웹 응용 프로그램은 종종 보안이 중요 한 데이터를 저장 해야 합니다. Windows는 데스크탑 응용 프로그램을 위한 DPAPI를 제공하지만 웹 응용 프로그램에는 적합하지 않습니다. ASP.NET Core 데이터 보호 스택의 개발자 키 관리 및 회전을 포함 한 데이터를 보호 사용할 수 있는 간단 하 고 사용 하기 쉬운 암호화 API를 제공 합니다.

ASP.NET Core 데이터 보호 스택은 장기적으로 ASP.NET 1.x - 4.x의 <machineKey> 요소를 대체하기 위한 목적으로 설계되었습니다. 기존 암호화 스택의 많은 단점을 해결하는 한편, 현대적인 응용 프로그램에서 접할 수 있는 대부분의 사용 사례에 즉각적으로 대응할 수 있는 솔루션을 제공하도록 설계되었습니다.

## <a name="problem-statement"></a>문제 설명

전체적인 문제를 다음 한 문장으로 간단 명료하게 정리할 수 있습니다: 나중에 검색에 대 한 신뢰할 수 있는 정보를 유지 해야 하지만 지 속성 메커니즘이 신뢰 하지 않습니다. 웹의 관점에서 다시 말하자면 "신뢰할 수 있는 상태를 신뢰할 수 없는 클라이언트를 통해서 왕복해야(Round-Trip) 한다"고 할 수 있습니다."

대표적인 사례가 인증 쿠키나 전달자 토큰(Bearer Token)의 경우입니다. 서버가 "나는 Groot고 xyz 권한을 갖고 있다"라는 토큰을 생성해서 클라이언트로 전달합니다. 이후 특정 시점에 클라이언트가 다시 서버로 해당 토큰을 제출하지만 서버로서는 클라이언트가 해당 토큰을 변조하지 않았다는 어떤한 보장이 필요합니다. 따라서 필요한 첫 번째 요건은 신뢰성(Authenticity)입니다(무결성(Integrity) 또는 변조 방지(Tamper-Proofing)하고도 합니다).

그리고 저장된 상태(정보)를 신뢰하는 주체는 서버이므로, 이 상태에 운영 환경 고유의 정보가 포함되어 있을 수도 있음을 예상할 수 있습니다. 이 정보는 파일 경로, 권한, 핸들 혹은 그 밖의 간접 참조, 또는 서버 고유의 데이터 중 일부 같은 형태를 갖출 수도 있습니다. 일반적으로 이런 정보들은 신뢰할 수 없는 클라이언트에게는 공개되지 않습니다. 따라서 필요한 두 번째 요건은 기밀성(Confidentiality)입니다.

마지막으로 현대적 응용 프로그램은 구성 요소를 기반으로 구축되므로 각 개별 구성 요소는 시스템의 다른 구성 요소들과 관계없이 이 시스템(데이터 보호 스택)을 활용할 수 있어야 합니다. 예를 들어, 전달자 토큰 구성 요소가 데이터 보호 스택을 사용한다면 역시 같은 스택을 사용하는 CSRF 방지 메커니즘의 간섭없이 동작할 수 있어야 합니다. 따라서 필요한 마지막 요건은 격리(Isolation)입니다.

더 많은 제약 조건을 규정해서 필요 요건의 범위를 좁힐 수 있습니다. 암호화 시스템 내에서 동작하는 모든 서비스를 동등하게 신뢰할 수 있으며, 직접 제어하는 서비스 외부에서 데이터가 생성되거나 사용될 필요가 없다고 가정합니다. 또한, 웹 서비스에 대한 각 요청이 암호화 시스템을 여러 번 거칠 수도 있기 때문에 최대한 빠르게 작업을 처리해야 합니다. 결론적으로 이런 시나리오에는 대칭 암호화가 적합하며, 필요해질 때까지 비대칭 암호화에 대해서는 무시할 수 있습니다.

## <a name="design-philosophy"></a>디자인 원칙

먼저 우리는 기존 스택과 관련된 문제점을 확인하는 작업에 착수했습니다. 이 작업을 마치고 기존 솔루션의 현황을 조사해본 결과, 기존 솔루션에는 원하는 기능들이 전혀 존재하지 않는다는 결론을 내렸습니다. 이후, 다음과 같은 몇 가지 기본 원칙에 따라 솔루션을 설계했습니다.

* 시스템 구성 방식이 간단해야 합니다. 이상적으로는 특별히 시스템을 구성하지 않고도(Zero-Configuration) 개발자들이 작업하는 데 전혀 지장이 없어야 합니다. 개발자가 특정 측면(예: 키 저장소)을 구성해야 할 경우, 해당 특정 구성을 간단히 처리할 수 있는 방법이 제공되어야 합니다.

* 간단한 소비자 지향적인 API를 제공해야 합니다. 이 API는 올바르게 사용하기는 쉽고 잘못 사용하기는 어려워야 합니다.

* 개발자는 키 관리 원칙 배울 하지 않아야 합니다. 시스템이 개발자 대신 알고리즘을 선택하고 키의 수명을 처리해야 합니다. 이상적으로는 개발자가 가공되지 않은 키 자료에 접근할 필요조차 없어야 합니다.

* 가능하다면 저장된 비활성 키를 보호해야 합니다. 또한, 시스템이 적절한 기본 보호 메커니즘을 찾아서 이를 자동으로 적용해야 합니다.

이러한 원칙을 염두 우리는 간단한 개발 [사용 하기 쉬운](xref:security/data-protection/using-data-protection) 데이터 보호 스택의 합니다.

ASP.NET Core 데이터 보호 API는 기밀 페이로드를 무기한 저장하기 위한 의도로 설계되지 않았습니다. 무기한 저장 시나리오에는 [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) 나 [Azure 권한 관리](https://docs.microsoft.com/rights-management/) 같은 다른 기술이 더 적합하며, 이런 기술들은 그에 상응하는 강력한 키 관리 기능을 갖추고 있습니다. 즉, 개발자는 ASP.NET Core 데이터 보호 Api를 사용 하 여 기밀 데이터의 장기 보호에 대 한 일은 없습니다.

## <a name="audience"></a>대상 사용자

데이터 보호 시스템은 다섯 가지 주요 패키지로 구분됩니다. 이 API들의 다양한 측면들은 세 가지 주요 대상 그룹을 목표로 합니다.

1. [소비자 Api 개요](xref:security/data-protection/consumer-apis/overview) 대상 프레임 워크 및 응용 프로그램 개발자.

   "싶지 스택 작동 하는 방법에 대 한 또는 구성 된 방식에 대 한 자세한 내용을 알아보려면 합니다. 단지 API를 성공적으로 사용할 개연성이 높은 가장 간단한 방법으로 특정 작업을 수행하기만 하면 됩니다."

2. [구성 Api](xref:security/data-protection/configuration/overview) 응용 프로그램 개발자 및 시스템 관리자가 대상으로 합니다.

   "내가 작업 중인 환경이 기본 경로가 아니거나 별도의 설정을 필요로 한다는 점을 데이터 보호 시스템에게 알릴 필요가 있습니다."

3. 확장성 API는 사용자 지정 정책 구현을 담당하는 개발자를 대상으로 합니다. 이런 API들을 사용해야 하는 경우는 드물며, 경험이 풍부한 보안 인식이 높은 개발자들만을 대상으로 국한됩니다.

   "나는 매우 독특한 동작 요건 때문에 시스템 내의 전체 구성 요소를 교체해야 합니다. 요건을 만족하는 플러그인을 구축하기 위해서 일반적으로는 잘 사용되지 않는 API 표면을 배우려고 합니다."

## <a name="package-layout"></a>패키지 레이아웃

데이터 보호 스택은 다섯 개의 패키지로 구성됩니다.

* Microsoft.AspNetCore.DataProtection.Abstractions 패키지에는 가장 기본이 되는 IDataProtectionProvider 인터페이스와 IDataProtector 인터페이스가 포함되어 있습니다. 그리고 추가적으로 이 형식들을 이용한 작업을 보조해주는 유용한 확장 메서드들이 함께 포함되어 있습니다(예: IDataProtector.Protect의 오버로드). 자세한 정보는 소비자 인터페이스 섹션을 참조하세요. 다른 누군가가 데이터 보호 시스템의 인스턴스를 생성하는 역할을 수행하고, 여러분은 단지 API를 사용하기만 한다면 Microsoft.AspNetCore.DataProtection.Abstractions 패키지를 참조하면 됩니다.

* Microsoft.AspNetCore.DataProtection 패키지에는 핵심 암호화 작업, 키 관리, 구성 및 확장성 같은 데이터 보호 시스템의 중추를 구성하는 구현들이 포함되어 있습니다. 데이터 보호 시스템의 인스턴스를 생성해야 한다거나(예: IServiceCollection에 추가하는 등), 그 동작을 변경 또는 확장해야 한다면 Microsoft.AspNetCore.DataProtection 패키지를 참조해야 합니다.

* Microsoft.AspNetCore.DataProtection.Extensions 패키지에는 개발자가 유용하게 사용할 수 있지만 핵심 패키지에는 속하지 않는 추가적인 API들이 포함되어 있습니다. 예를 들어, 이 패키지에는 "종속성 주입 설정 없이 특정 키 저장소 디렉터리를 가리키는 시스템의 인스턴스를 생성하는" 간단한 API가 포함되어 있습니다. 또한, 보호되는 페이로드의 수명을 제한하는 확장 메서드도 여기에 포함되어 있습니다.

* Microsoft.AspNetCore.DataProtection.SystemWeb 패키지를 기존의 ASP.NET 4.x 응용 프로그램에 설치하면 그 내부의 <machineKey> 처리 대신 새로운 데이터 보호 스택을 사용하도록 재지정할 수 있습니다. 보다 자세한 정보는 [호환성](xref:security/data-protection/compatibility/replacing-machinekey#compatibility-replacing-machinekey) 을 참고하시기 바랍니다.

* Microsoft.AspNetCore.Cryptography.KeyDerivation 패키지는 PBKDF2 비밀번호 해싱 루틴 구현을 제공하며 사용자의 비밀번호를 안전하게 처리해야 하는 시스템에서 사용할 수 있습니다. 참조 [암호 해시](xref:security/data-protection/consumer-apis/password-hashing) 자세한 정보에 대 한 합니다.
