---
title: ASP.NET Core의 용도 계층 구조 및 다중 테넌트
author: rick-anderson
description: ASP.NET Core 데이터 보호 Api에 대 한 관계로 용도 문자열 계층 구조 및 다중 테 넌 트에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/purpose-strings-multitenancy
ms.openlocfilehash: 1133d40e7b325d58b3f70e7387494dae36ff8ac9
ms.sourcegitcommit: fd461c60b5e36c7019f81da0138cc859d0fddaa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/10/2018
ms.locfileid: "41827517"
---
# <a name="purpose-hierarchy-and-multi-tenancy-in-aspnet-core"></a>ASP.NET Core의 용도 계층 구조 및 다중 테넌트

내부적으로는 `IDataProtector` 역시 `IDataProtectionProvider`이기 때문에 서로 연이어 용도를 연결할 수 있습니다. 그런 관점에서 본다면 `provider.CreateProtector([ "purpose1", "purpose2" ])` 와 `provider.CreateProtector("purpose1").CreateProtector("purpose2")` 는 서로 동일합니다.

그리고 이런 특징을 이용해서 데이터 보호 시스템 내부에 흥미로운 계층 관계를 구성할 수 있습니다. 이전 문서에서 간단히 살펴봤던 [Contoso.Messaging.SecureMessage](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-contoso-purpose) 예제의 경우, SecureMessage 구성 요소는 먼저 `provider.CreateProtector("Contoso.Messaging.SecureMessage")` 를 한 번 호출한 다음, 그 결과를 `_myProvider` 라는 이름의 private 필드에 캐시해 놓을 수 있습니다. 그런 다음, 이후에 생성하는 보호자들은 `_myProvider.CreateProtector("User: username")` 을 호출해서 생성할 수 있으며, 이렇게 만들어진 보호자를 개별 메시지 보안에 사용할 수 있습니다.

이 관계를 반대로 뒤집어 볼 수도 있습니다. 다중 테넌트를 호스트하는 단일 논리 응용 프로그램이 존재하고 (CMS 등의), 각 테넌트가 자체적으로 인증 및 상태 관리 시스템을 구성할 수 있다고 가정해보겠습니다. 최상위 응용 프로그램에는 단일 마스터 공급자가 존재하고 `provider.CreateProtector("Tenant 1")` 및 `provider.CreateProtector("Tenant 2")` 를 호출해서 각 테넌트에게 자체적으로 격리된 데이터 보호 시스템을 제공합니다. 그러면 테넌트는 필요에 따라 자신만의 개별적인 보호자를 파생해서 생성할 수는 있지만, 그 어떤 방법을 쓰더라도 시스템 내부의 다른 테넌트와 충돌하는 보호자를 생성할 수는 없습니다. 이를 도식으로 표현하면 다음과 같습니다.

![다중 테넌트 용도](purpose-strings-multitenancy/_static/purposes-multi-tenancy.png)

>[!WARNING]
> 여기서는 최상위 응용 프로그램이 각각의 테넌트가 사용할 수 있는 API를 제어할 수 있고, 각 테넌트는 서버에서 임의의 코드를 실행할 수 없다고 가정합니다. 만약 테넌트가 임의의 코드를 실행할 수 있다면 내부적으로 리플렉션을 수행해서 격리 보장을 깨뜨리거나 마스터 키 관련 자료를 직접 읽어서 원하는 하위 키를 파생할 수 있습니다.

데이터 보호 시스템은 기본으로 제공되는 구성 하에서 사실상 일종의 다중 테넌트를 사용합니다. 기본적으로 마스터 키 관련 자료는 작업자 프로세스 계정의 사용자 프로필 폴더에, 또는 IIS 응용 프로그램 풀 신원의 경우 레지스트리에 저장됩니다. 그러나 실제로는 단일 계정으로 여러 개의 응용 프로그램들을 실행하는 것이 일반적이므로 결과적으로 해당하는 모든 응용 프로그램들이 마스터 키 관련 자료를 공유하게 됩니다. 이런 문제점을 해결하기 위해서 데이터 보호 시스템은 응용 프로그램별로 고유한 식별자를 전체 용도 체인의 첫 번째 요소로 자동으로 삽입합니다. 이 암시적 용도로 인해서 각 응용 프로그램은 시스템 내에서 고유한 테넌트로 효과적으로 처리되어 [각각의 응용 프로그램들이 서로 격리](xref:security/data-protection/configuration/overview#per-application-isolation) 되며, 보호자 생성 프로세스가 위의 이미지와 동일한 형태를 띄게 됩니다.
