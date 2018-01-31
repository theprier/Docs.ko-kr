---
title: "해당 레지스트리 키가 해지 한 보호 해제 페이로드"
author: rick-anderson
description: "이 문서에서는 이후로 해지 된, ASP.NET Core 응용 프로그램의 키로 보호 된 데이터를 보호 해제 하는 방법을 설명 합니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/consumer-apis/dangerous-unprotect
ms.openlocfilehash: 584dbb545c15add4401086b9160d4bf30caf41b5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="unprotecting-payloads-whose-keys-have-been-revoked"></a>해당 레지스트리 키가 해지 한 보호 해제 페이로드

<a name="data-protection-consumer-apis-dangerous-unprotect"></a>

ASP.NET Core 데이터 보호 Api는 주로 없습니다 기밀 페이로드의 무한 지 속성. 와 같은 다른 기술은 [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) 및 [Azure 권한 관리](https://docs.microsoft.com/rights-management/) 무한 저장소 시나리오에 보다 적합 한까지 강력한 키 관리 기능을 갖습니다. 즉, 개발자는 ASP.NET Core 데이터 보호 Api를 사용 하 여 기밀 데이터의 장기 보호에 대 한 일은 없습니다. 키가 키 링에서 하므로 제거 하지 `IDataProtector.Unprotect` 으로 키가 사용 가능 하 고 유효한에 항상 기존 페이로드를 복구할 수 있습니다.

개발자가으로 해지 된 키로 보호 된 데이터의 보호를 해제 하려고 할 때 문제가 발생 하는 반면 `IDataProtector.Unprotect` 이 경우 예외가 throw 됩니다. 이러한 종류의 페이로드 쉽게 다시 만들 수는 시스템에 의해와 사이트 방문자가 다시 로그인 하려면 최악의 해야 할 수 있습니다 (예: 인증 토큰의 경우) 단기 / 임시 페이로드 실험용 수 있습니다. 하지만 발생 하는 지속형 페이로드 `Unprotect` throw 하지 않은 데이터 손실 될 수 있습니다.

## <a name="ipersisteddataprotector"></a>IPersistedDataProtector

데이터 보호 시스템에 포함 되도록 키 해지 된 경우에 보호 된 페이로드를 허용할 때의 시나리오를 지원 하려면는 `IPersistedDataProtector` 유형입니다. 인스턴스를 가져오려면 `IPersistedDataProtector`, 단순히의 인스턴스를 가져올 `IDataProtector` 평소와 같이 및 try 캐스트에는 `IDataProtector` 를 `IPersistedDataProtector`합니다.

> [!NOTE]
> 일부 `IDataProtector` 인스턴스를 캐스팅할 수 있습니다 `IPersistedDataProtector`합니다. As 연산자는 C# 개발자가 사용 해야 하거나 런타임 예외를 방지 하기 위해 잘못 된 캐스팅 하 여 발생 한 되어야 할 유사한 처리할 준비가 실패 하는 경우 적절 하 게 합니다.

`IPersistedDataProtector`다음 API 화면을 노출합니다.

```csharp
DangerousUnprotect(byte[] protectedData, bool ignoreRevocationErrors,
     out bool requiresMigration, out bool wasRevoked) : byte[]
```

이 API (바이트 배열)로 보호 된 페이로드 하며 보호 되지 않는 페이로드를 반환 합니다. 문자열 기반 오버 로드가 없습니다. Out 매개 변수 2는 다음과 같습니다.

* `requiresMigration`:이 페이로드를 보호 하는 데 더 이상 활성 기본 키, 예:이 페이로드를 보호 하는 데 사용 된 키가 이전 및 이후 작업 롤링 키에 있는 경우 true로 설정 수행 될 위치입니다. 호출자에 게 비즈니스 요구에 따라 페이로드를 다시 보호 하는 것이 좋습니다. 할 수 있습니다.

* `wasRevoked`:이 페이로드를 보호 하기 위해 사용 되는 키가 해지 하는 경우 true로 설정 됩니다.

>[!WARNING]
> 전달 하는 경우 각별히 주의 해 `ignoreRevocationErrors: true` 에 `DangerousUnprotect` 메서드. 이 메서드를 호출한 경우에는 `wasRevoked` 값이 true 이면이 페이로드를 보호 하기 위해 사용 되는 키가 해지 되 고 페이로드의 신뢰성 주의 대상으로 처리 되어야 합니다. 이 경우에 작업을 계속 보호 되지 않는 페이로드에 임을 인증, 예를 들어 일부 별도 보증을 사용 하는 경우 신뢰할 수 없는 웹 클라이언트에서 전송 되는 것이 아니라 보안 데이터베이스에서 온 것인지 합니다.

[!code-csharp[Main](dangerous-unprotect/samples/dangerous-unprotect.cs)]
