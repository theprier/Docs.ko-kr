---
title: 기타 ASP.NET Core 데이터 보호 Api
author: rick-anderson
description: ASP.NET Core 데이터 보호 ISecret 인터페이스에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 484c6a0979a10e7cf2b801873655caa99a42532c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30072766"
---
# <a name="miscellaneous-aspnet-core-data-protection-apis"></a><span data-ttu-id="9207d-103">기타 ASP.NET Core 데이터 보호 Api</span><span class="sxs-lookup"><span data-stu-id="9207d-103">Miscellaneous ASP.NET Core Data Protection APIs</span></span>

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> <span data-ttu-id="9207d-104">다음 인터페이스 중 하나를 구현 하는 형식은 스레드로부터 안전 해야 합니다. 여러 호출자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="9207d-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="9207d-105">ISecret</span></span>

<span data-ttu-id="9207d-106">`ISecret` 인터페이스 예: 암호화 키 자료의 비밀 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-106">The `ISecret` interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="9207d-107">다음 API 화면을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-107">It contains the following API surface:</span></span>

* <span data-ttu-id="9207d-108">`Length`: `int`</span><span class="sxs-lookup"><span data-stu-id="9207d-108">`Length`: `int`</span></span>

* <span data-ttu-id="9207d-109">`Dispose()`: `void`</span><span class="sxs-lookup"><span data-stu-id="9207d-109">`Dispose()`: `void`</span></span>

* <span data-ttu-id="9207d-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span><span class="sxs-lookup"><span data-stu-id="9207d-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span></span>

<span data-ttu-id="9207d-111">`WriteSecretIntoBuffer` 메서드는 원시 암호 값을 사용 하 여 제공 된 버퍼를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-111">The `WriteSecretIntoBuffer` method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="9207d-112">이 API는 매개 변수로 버퍼를 사용 하는 이유 반환 하는 대신 한 `byte[]` 직접는이 기회 호출자에 게는 관리 되는 가비지 수집기에 대 한 보안 노출을 제한 하는 버퍼 개체를 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-112">The reason this API takes the buffer as a parameter rather than returning a `byte[]` directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="9207d-113">`Secret` 형식이의 구체적인 구현을 `ISecret` 비밀 값 처리 중인 메모리에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-113">The `Secret` type is a concrete implementation of `ISecret` where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="9207d-114">Windows 플랫폼에서 암호 값이를 통해 암호화 [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9207d-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>
