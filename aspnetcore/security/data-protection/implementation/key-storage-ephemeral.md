---
title: ASP.NET Core에서 임시 데이터 보호 공급자
author: rick-anderson
description: ASP.NET Core 임시 데이터 보호 공급자의 구현 세부 정보에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: e4b0014ab3bdbf90b91383e8a33102f94faa8153
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36279469"
---
# <a name="ephemeral-data-protection-providers-in-aspnet-core"></a>ASP.NET Core에서 임시 데이터 보호 공급자

<a name="data-protection-implementation-key-storage-ephemeral"></a>

시나리오에서 응용 프로그램 해야는 throwaway `IDataProtectionProvider`합니다. 예를 들어 일회용 콘솔 응용 프로그램에서는 개발자를 시험만 될 수 있습니다 또는 응용 프로그램 자체는 임시로 (스크립팅 되었으므로 또는 단위 테스트 프로젝트). 이러한 시나리오를 지원 하기 위해는 [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) 패키지에 포함 된 유형을 `EphemeralDataProtectionProvider`합니다. 이 형식은의 기본 구현을 제공 `IDataProtectionProvider` 키 리포지토리가 전적으로 메모리에 유지 되 고 백업 저장소에 기록 되지 않습니다.

각 인스턴스에 `EphemeralDataProtectionProvider` 자체의 고유한 마스터 키를 사용 합니다. 따라서 경우는 `IDataProtector` 에서 시작 하는 `EphemeralDataProtectionProvider` 보호 된 페이로드를 생성 합니다. 해당 페이로드의 해당에 의해 보호만 수 `IDataProtector` (동일한 [목적](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes) 체인)에서 동일한 루트 `EphemeralDataProtectionProvider` 인스턴스입니다.

다음 예제에서는 인스턴스화는 `EphemeralDataProtectionProvider` 보호 및 데이터를 보호 해제 하는 데 사용 하 합니다.

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
