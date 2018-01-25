---
title: "보호 된 페이로드의 수명을 제한"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core 데이터 보호 Api를 사용 하 여 보호 된 페이로드의 수명을 제한 하는 방법을 설명 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/limited-lifetime-payloads
ms.openlocfilehash: 7909f21057f22e78c03b41464a19a18ce0908216
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="limiting-the-lifetime-of-protected-payloads"></a>보호 된 페이로드의 수명을 제한

응용 프로그램 개발자가 설정된 된 시간 동안 후에 만료 되는 보호 된 페이로드를 작성 하려고 하는 위치 시나리오가 있습니다. 예를 들어, 보호 된 페이로드는 1 시간 동안 유효 해야만 암호 다시 설정 토큰을 나타낼 수 있습니다. 개발자는 포함 된 만료 날짜를 포함 하는 고유한 페이로드 형식을 만들 수에 대 한 수 및 고급 개발자를 누르고, 이렇게 할 수 있습니다 이지만 대부분 개발자의 이러한 만료 관리 수 커집니다 번거로운.

패키지 대상 우리의 개발자에 대 한 더 쉽게 확인 하려면 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) 설정 시간이 지나면 자동으로 만료 되는 페이로드를 만들기 위한 유틸리티 Api를 포함 합니다. 이러한 Api의 오프 중지는 `ITimeLimitedDataProtector` 유형입니다.

## <a name="api-usage"></a>API 사용

`ITimeLimitedDataProtector` 인터페이스는 보호 하 고, 시간이 제한 된 / 자동으로 만료 되는 페이로드를 보호 해제에 대 한 핵심 인터페이스입니다. 인스턴스를 만드는 `ITimeLimitedDataProtector`, 일반의 인스턴스를 먼저 해야 [IDataProtector](overview.md) 특정 용도 사용 하 여 생성 합니다. 한 번의 `IDataProtector` 인스턴스를 사용할 수 있는 호출에서 `IDataProtector.ToTimeLimitedDataProtector` 기본 만료 기능 다시 보호기를 가져올 확장 메서드를 합니다.

`ITimeLimitedDataProtector`다음과 같은 API 화면 및 확장 메서드를 노출합니다.

* CreateProtector (문자열 용도): ITimeLimitedDataProtector-이 API는 기존 비슷합니다 `IDataProtectionProvider.CreateProtector` 만들기를 사용할 수 있다는 점에서 [체인의 용도 위해](purpose-strings.md) 루트 시간이 제한 된 보호기를 합니다.

* Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]

* Protect(byte[] plaintext, TimeSpan lifetime) : byte[]

* (바이트 일반 텍스트)를 보호: byte

* (문자열 일반 텍스트, DateTimeOffset 만료) 보호: 문자열

* 보호 (문자열 일반 텍스트, TimeSpan 수명): 문자열

* (문자열 일반 텍스트)를 보호: 문자열

핵심 외에도 `Protect` 의 일반 텍스트만 수행 하는 메서드는 페이로드의 만료 날짜를 지정할 수 있는 새로운 오버 로드가 있습니다. 만료 날짜는 절대 날짜로 지정할 수 있습니다 (통해는 `DateTimeOffset`) 또는 상대 시간 (현재 시스템에서 시간을 통해는 `TimeSpan`). 만료 날짜를 사용 하지 않습니다는 오버 로드를 호출 하면 페이로드 가정 하지 만료 합니다.

* Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]

* Unprotect(byte[] protectedData) : byte[]

* (DateTimeOffset 만료 아웃 문자열 protectedData)를 보호 해제: 문자열

* (문자열 protectedData)를 보호 해제: 문자열

`Unprotect` 메서드 원래 보호 되지 않는 데이터를 반환 합니다. 페이로드 아직 만료 되지 않았는지, 절대 만료를 선택적 출력 매개 변수는 원래 보호 되지 않는 데이터와 함께 반환 됩니다. 페이로드 만료 되 면 CryptographicException Unprotect 메서드의 모든 오버 로드에 throw 됩니다.

>[!WARNING]
> 장기 또는 무기한 보존 해야 하는 페이로드를 보호 하기 위해 이러한 Api를 사용 하는 권장 되지 않습니다. 했습니다. "있습니까 여유가 한 달이 지난 후 영구적으로 복구할 수 없게 하려면 보호 된 페이로드"? 바람직한 방법은;으로 사용할 수 있습니다. 대답 한 경우 다음 없습니다 개발자 대체 Api를 고려해 야 합니다.

사용 하 여 아래 샘플은 [DI 아닌 코드 경로](../configuration/non-di-scenarios.md) 데이터 보호 시스템을 인스턴스화하기 위한 합니다. 이 샘플을 실행 하려면 먼저 Microsoft.AspNetCore.DataProtection.Extensions 패키지에 대 한 참조를 추가 했는지 확인 합니다.

[!code-csharp[Main](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]
