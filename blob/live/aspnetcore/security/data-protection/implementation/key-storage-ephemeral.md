---
title: "임시 데이터 보호 공급자"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core 임시 데이터 보호 공급자의 구현 세부 사항을 설명 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: 9c1d03373c9d7fb6dffb3583c58aa593fd3875f4
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="ephemeral-data-protection-providers"></a><span data-ttu-id="1aa8c-103">임시 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="1aa8c-103">Ephemeral data protection providers</span></span>

<a name="data-protection-implementation-key-storage-ephemeral"></a>

<span data-ttu-id="1aa8c-104">시나리오에서 응용 프로그램 해야는 throwaway `IDataProtectionProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-104">There are scenarios where an application needs a throwaway `IDataProtectionProvider`.</span></span> <span data-ttu-id="1aa8c-105">예를 들어 일회용 콘솔 응용 프로그램에서는 개발자를 시험만 될 수 있습니다 또는 응용 프로그램 자체는 임시로 (스크립팅 되었으므로 또는 단위 테스트 프로젝트).</span><span class="sxs-lookup"><span data-stu-id="1aa8c-105">For example, the developer might just be experimenting in a one-off console application, or the application itself is transient (it's scripted or a unit test project).</span></span> <span data-ttu-id="1aa8c-106">이러한 시나리오를 지원 하기 위해는 [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) 패키지에 포함 된 유형을 `EphemeralDataProtectionProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-106">To support these scenarios the [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) package includes a type `EphemeralDataProtectionProvider`.</span></span> <span data-ttu-id="1aa8c-107">이 형식은의 기본 구현을 제공 `IDataProtectionProvider` 키 리포지토리가 전적으로 메모리에 유지 되 고 백업 저장소에 기록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-107">This type provides a basic implementation of `IDataProtectionProvider` whose key repository is held solely in-memory and isn't written out to any backing store.</span></span>

<span data-ttu-id="1aa8c-108">각 인스턴스에 `EphemeralDataProtectionProvider` 자체의 고유한 마스터 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-108">Each instance of `EphemeralDataProtectionProvider` uses its own unique master key.</span></span> <span data-ttu-id="1aa8c-109">따라서 경우는 `IDataProtector` 에서 시작 하는 `EphemeralDataProtectionProvider` 보호 된 페이로드를 생성 합니다. 해당 페이로드의 해당에 의해 보호만 수 `IDataProtector` (동일한 [목적](../consumer-apis/purpose-strings.md#data-protection-consumer-apis-purposes) 체인)에서 동일한 루트 `EphemeralDataProtectionProvider` 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-109">Therefore, if an `IDataProtector` rooted at an `EphemeralDataProtectionProvider` generates a protected payload, that payload can only be unprotected by an equivalent `IDataProtector` (given the same [purpose](../consumer-apis/purpose-strings.md#data-protection-consumer-apis-purposes) chain) rooted at the same `EphemeralDataProtectionProvider` instance.</span></span>

<span data-ttu-id="1aa8c-110">다음 예제에서는 인스턴스화는 `EphemeralDataProtectionProvider` 보호 및 데이터를 보호 해제 하는 데 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa8c-110">The following sample demonstrates instantiating an `EphemeralDataProtectionProvider` and using it to protect and unprotect data.</span></span>

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
