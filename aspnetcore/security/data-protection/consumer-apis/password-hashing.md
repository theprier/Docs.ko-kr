---
title: "비밀번호 해싱"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core의 데이터 보호 API를 사용해서 비밀번호를 해싱하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: 8e2796108be14ef382f46e6deb3d584517120d27
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="password-hashing"></a><span data-ttu-id="5596f-103">비밀번호 해싱</span><span class="sxs-lookup"><span data-stu-id="5596f-103">Password Hashing</span></span>

<span data-ttu-id="5596f-104">데이터 보호 코드 베이스에는 암호화 키 파생 함수를 제공해주는 *Microsoft.AspNetCore.Cryptography.KeyDerivation* 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-104">The data protection code base includes a package *Microsoft.AspNetCore.Cryptography.KeyDerivation* which contains cryptographic key derivation functions.</span></span> <span data-ttu-id="5596f-105">이 패키지는 독립적인 구성 요소로서 데이터 보호 시스템의 나머지 다른 부분에 의존하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-105">This package is a standalone component and has no dependencies on the rest of the data protection system.</span></span> <span data-ttu-id="5596f-106">이 패키지는 완벽히 독립적으로 사용이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-106">It can be used completely independently.</span></span> <span data-ttu-id="5596f-107">다만 편의상 소스가 데이터 보호 코드 베이스와 함께 위치해 있을 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-107">The source exists alongside the data protection code base as a convenience.</span></span>

<span data-ttu-id="5596f-108">이 패키지는 [PBKDF2 알고리즘](https://tools.ietf.org/html/rfc2898#section-5.2)을 이용해서 비밀번호 해싱을 수행하는 `KeyDerivation.Pbkdf2` 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-108">The package currently offers a method `KeyDerivation.Pbkdf2` which allows hashing a password using the [PBKDF2 algorithm](https://tools.ietf.org/html/rfc2898#section-5.2).</span></span> <span data-ttu-id="5596f-109">이 API는 .NET 프레임워크의 기존 [Rfc2898DeriveBytes 형식](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes)과 매우 유사하지만, 세 가지 중요한 차이점이 존재합니다:</span><span class="sxs-lookup"><span data-stu-id="5596f-109">This API is very similar to the .NET Framework's existing [Rfc2898DeriveBytes type](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), but there are three important distinctions:</span></span>

1. <span data-ttu-id="5596f-110">`KeyDerivation.Pbkdf2` 메서드는 다양한 PRF를 사용할 수 있는 반면 (현재 `HMACSHA1`, `HMACSHA256`, 그리고 `HMACSHA512`를 지원), `Rfc2898DeriveBytes` 형식은 `HMACSHA1`만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-110">The `KeyDerivation.Pbkdf2` method supports consuming multiple PRFs (currently `HMACSHA1`, `HMACSHA256`, and `HMACSHA512`), whereas the `Rfc2898DeriveBytes` type only supports `HMACSHA1`.</span></span>

2. <span data-ttu-id="5596f-111">`KeyDerivation.Pbkdf2` 메서드는 현재 운영 체제를 감지해서 가장 최적화된 구현 루틴을 선택하기 때문에 상황에 따라 훨씬 향상된 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-111">The `KeyDerivation.Pbkdf2` method detects the current operating system and attempts to choose the most optimized implementation of the routine, providing much better performance in certain cases.</span></span> <span data-ttu-id="5596f-112">(Windows 8에서 `Rfc2898DeriveBytes`보다 약 10배에 가까운 성능을 보여줍니다.)</span><span class="sxs-lookup"><span data-stu-id="5596f-112">(On Windows 8, it offers around 10x the throughput of `Rfc2898DeriveBytes`.)</span></span>

3. <span data-ttu-id="5596f-113">`KeyDerivation.Pbkdf2` 메서드는 호출자가 모든 매개 변수를 지정해야 합니다 (솔트, PRF, 그리고 반복 횟수까지).</span><span class="sxs-lookup"><span data-stu-id="5596f-113">The `KeyDerivation.Pbkdf2` method requires the caller to specify all parameters (salt, PRF, and iteration count).</span></span> <span data-ttu-id="5596f-114">반면 `Rfc2898DeriveBytes` 형식은 이에 대한 기본값들을 제공해줍니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-114">The `Rfc2898DeriveBytes` type provides default values for these.</span></span>

[!code-csharp[](password-hashing/samples/passwordhasher.cs)]

<span data-ttu-id="5596f-115">실제 사용 사례를 살펴보려면 ASP.NET Core Identity의 `PasswordHasher` 형식의 소스 코드를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="5596f-115">See the source code for ASP.NET Core Identity's `PasswordHasher` type for a real-world use case.</span></span>
