---
title: "암호 해시"
author: rick-anderson
description: "이 문서에는 ASP.NET Core 데이터 보호 Api를 사용 하 여 암호를 해시 하는 방법을 설명 합니다."
keywords: "ASP.NET Core, 데이터 보호, 암호 해시"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 982a1eb2-1e6f-4909-896f-82784364472d
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: da9f505f58f18f7ab3b93753bae079eb976b3939
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="password-hashing"></a><span data-ttu-id="c011e-104">암호 해시</span><span class="sxs-lookup"><span data-stu-id="c011e-104">Password Hashing</span></span>

<span data-ttu-id="c011e-105">패키지를 포함 하는 데이터 보호 코드 베이스 *Microsoft.AspNetCore.Cryptography.KeyDerivation* 는 암호화 키 파생 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-105">The data protection code base includes a package *Microsoft.AspNetCore.Cryptography.KeyDerivation* which contains cryptographic key derivation functions.</span></span> <span data-ttu-id="c011e-106">이 패키지는 독립 실행형 구성 요소와 데이터 보호 시스템의 나머지 부분에 의존 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-106">This package is a standalone component and has no dependencies on the rest of the data protection system.</span></span> <span data-ttu-id="c011e-107">사용할 수 없습니다 완전히 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-107">It can be used completely independently.</span></span> <span data-ttu-id="c011e-108">소스 편의 위해 기본 데이터 보호 코드와 함께 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-108">The source exists alongside the data protection code base as a convenience.</span></span>

<span data-ttu-id="c011e-109">패키지는 현재 메서드를 제공 `KeyDerivation.Pbkdf2` 사용 하 여 암호 해시를 허용 하는 [PBKDF2 알고리즘](https://tools.ietf.org/html/rfc2898#section-5.2)합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-109">The package currently offers a method `KeyDerivation.Pbkdf2` which allows hashing a password using the [PBKDF2 algorithm](https://tools.ietf.org/html/rfc2898#section-5.2).</span></span> <span data-ttu-id="c011e-110">이 API는.NET Framework의 기존와 매우 유사 [Rfc2898DeriveBytes 형식](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), 하지만 세 가지 중요 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-110">This API is very similar to the .NET Framework's existing [Rfc2898DeriveBytes type](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), but there are three important distinctions:</span></span>

1. <span data-ttu-id="c011e-111">`KeyDerivation.Pbkdf2` 여러 PRFs 사용 방법은 지원 (현재 `HMACSHA1`, `HMACSHA256`, 및 `HMACSHA512`) 인 반면는 `Rfc2898DeriveBytes` 형식에서 지원만 `HMACSHA1`합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-111">The `KeyDerivation.Pbkdf2` method supports consuming multiple PRFs (currently `HMACSHA1`, `HMACSHA256`, and `HMACSHA512`), whereas the `Rfc2898DeriveBytes` type only supports `HMACSHA1`.</span></span>

2. <span data-ttu-id="c011e-112">`KeyDerivation.Pbkdf2` 메서드는 현재 운영 체제를 검색 하 고 특정 한 경우에 훨씬 더 나은 성능을 제공 하는 루틴의 가장 최적화 된 구현을 선택 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-112">The `KeyDerivation.Pbkdf2` method detects the current operating system and attempts to choose the most optimized implementation of the routine, providing much better performance in certain cases.</span></span> <span data-ttu-id="c011e-113">(Windows 8에서 약 10 배의 처리량을 제공 `Rfc2898DeriveBytes`.)</span><span class="sxs-lookup"><span data-stu-id="c011e-113">(On Windows 8, it offers around 10x the throughput of `Rfc2898DeriveBytes`.)</span></span>

3. <span data-ttu-id="c011e-114">`KeyDerivation.Pbkdf2` 메서드에 필요한 모든 매개 변수를 지정 하려면 호출자 (솔트, PRF, 및 반복 횟수).</span><span class="sxs-lookup"><span data-stu-id="c011e-114">The `KeyDerivation.Pbkdf2` method requires the caller to specify all parameters (salt, PRF, and iteration count).</span></span> <span data-ttu-id="c011e-115">`Rfc2898DeriveBytes` 유형 이들에 대 한 기본값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-115">The `Rfc2898DeriveBytes` type provides default values for these.</span></span>

[!code-csharp[Main](password-hashing/samples/passwordhasher.cs)]

<span data-ttu-id="c011e-116">ASP.NET Core Id에 대 한 소스 코드 참조 `PasswordHasher` 실제 환경에 대 한 입력 사례를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c011e-116">See the source code for ASP.NET Core Identity's `PasswordHasher` type for a real-world use case.</span></span>
