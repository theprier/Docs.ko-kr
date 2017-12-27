---
title: "보호된 페이로드의 수명 제한하기"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core 데이터 보호 API를 사용하여 보호된 페이로드의 수명을 제한하는 방법을 살펴봅니다."
keywords: "ASP.NET Core, 데이터 보호, 페이로드 수명"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 000175e2-10fc-43dd-bfc2-51e004b97b44
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/limited-lifetime-payloads
ms.openlocfilehash: 3fe2e97db118a92cf6fa003b9ce8a9dedf253136
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="limiting-the-lifetime-of-protected-payloads"></a>보호된 페이로드의 수명 제한하기

일부 시나리오에서는 응용 프로그램 개발자가 일정 시간 후에 만료되는 보호된 페이로드를 생성해야 할 수도 있습니다. 예를 들어, 비밀번호 재설정 토큰으로 사용되는 한 시간 동안만 유효한 보호된 페이로드 같은 경우를 들 수 있습니다. 물론 개발자가 내부적으로 만료 일자를 담고 있는 페이로드 형식을 직접 만드는 것도 불가능한 일은 아니고, 오히려 고급 개발자라면 이런 방식을 더 선호할 수도 있겠지만, 만료를 관리하는 이런 작업은 대다수 개발자에게는 번거러운 작업입니다.

개발자가 이런 작업을 손쉽게 처리할 수 있도록 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) 패키지에는 일정 시간 뒤에 자동으로 만료되는 페이로드를 생성하는 유틸리티 API들이 포함되어 있습니다. 이 API들은 `ITimeLimitedDataProtector` 형식에서 제공됩니다.

## <a name="api-usage"></a>API 사용 방법

`ITimeLimitedDataProtector` 인터페이스는 시간 제한/자체 만료 페이로드를 보호하거나 보호 해제하는 작업을 수행하기 위한 핵심 인터페이스입니다. `ITimeLimitedDataProtector`의 인스턴스를 생성하려면, 먼저 특정 용도를 지정해서 생성한 일반적인 [IDataProtector](overview.md)의 인스턴스가 필요합니다. `IDataProtector`의 인스턴스를 얻은 뒤에 `IDataProtector.ToTimeLimitedDataProtector` 확장 메서드를 호출해서 만료 기능이 내장된 보호자를 다시 얻습니다.

`ITimeLimitedDataProtector`는 다음과 같은 API 표면 및 확장 메서드를 노출합니다:

* CreateProtector(string purpose) : ITimeLimitedDataProtector - 이 API는 루트 시간 제한 보호자로부터 [용도 체인](purpose-strings.md)을 생성할 수 있다는 점에서 기존의 `IDataProtectionProvider.CreateProtector`와 비슷합니다.

* Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]

* Protect(byte[] plaintext, TimeSpan lifetime) : byte[]

* Protect(byte[] plaintext) : byte[]

* Protect(string plaintext, DateTimeOffset expiration) : string

* Protect(string plaintext, TimeSpan lifetime) : string

* Protect(string plaintext) : string

평문만 전달하는 핵심 `Protect` 메서드들과 페이로드의 만료 일자를 지정할 수 있는 새로운 오버로드 메서드들이 함께 제공됩니다. 만료 일자는 절대 일시 (`DateTimeOffset` 형식으로) 또는 상대적 시간으로 (현재 시스템 시간에 대한 `TimeSpan` 형식으로) 지정할 수 있습니다. 만료가 지정되지 않은 오버로드 메서드가 호출되면 페이로드가 만료되지 않는 것으로 간주됩니다.

* Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]

* Unprotect(byte[] protectedData) : byte[]

* Unprotect(string protectedData, out DateTimeOffset expiration) : string

* Unprotect(string protectedData) : string

`Unprotect` 메서드는 보호가 해제된 원본 데이터를 반환합니다. 페이로드가 아직 만료되지 않았다면 보호되지 않은 원본 데이터와 함께 절대 만료일시가 선택적 out 매개 변수를 통해서 함께 반환됩니다. 반면 이미 페이로드가 만료됐다면 모든 `Unprotect` 오버로드 메서드가 `CryptographicException`을 던집니다.

>[!WARNING]
> 이 API들을 이용해서 장기간 혹은 무기한 유지되어야 하는 페이로드를 보호하는 것은 바람직하지 않습니다. 경험적으로 "보호된 페이로드가 한 달 뒤에 영구적으로 복구할 수 없게 되더라도 감당할 수 있는가?"라는 질문이 좋은 판단의 기준이 될 수 있습니다. 만약 이 질문에 대한 답이 "아니오"라면 다른 API를 고려해봐야 합니다.

다음 예제는 데이터 보호 시스템의 인스턴스를 생성하기 위해서 [비-DI 코드 경로](../configuration/non-di-scenarios.md)를 사용합니다. 이 예제를 실행하려면, 먼저 Microsoft.AspNetCore.DataProtection.Extensions 패키지 참조를 추가해야 합니다.

[!code-csharp[Main](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]
