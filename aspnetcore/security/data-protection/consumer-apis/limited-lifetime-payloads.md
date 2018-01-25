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
# <a name="limiting-the-lifetime-of-protected-payloads"></a><span data-ttu-id="6a305-103">보호 된 페이로드의 수명을 제한</span><span class="sxs-lookup"><span data-stu-id="6a305-103">Limiting the lifetime of protected payloads</span></span>

<span data-ttu-id="6a305-104">응용 프로그램 개발자가 설정된 된 시간 동안 후에 만료 되는 보호 된 페이로드를 작성 하려고 하는 위치 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-104">There are scenarios where the application developer wants to create a protected payload that expires after a set period of time.</span></span> <span data-ttu-id="6a305-105">예를 들어, 보호 된 페이로드는 1 시간 동안 유효 해야만 암호 다시 설정 토큰을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-105">For instance, the protected payload might represent a password reset token that should only be valid for one hour.</span></span> <span data-ttu-id="6a305-106">개발자는 포함 된 만료 날짜를 포함 하는 고유한 페이로드 형식을 만들 수에 대 한 수 및 고급 개발자를 누르고, 이렇게 할 수 있습니다 이지만 대부분 개발자의 이러한 만료 관리 수 커집니다 번거로운.</span><span class="sxs-lookup"><span data-stu-id="6a305-106">It's certainly possible for the developer to create their own payload format that contains an embedded expiration date, and advanced developers may wish to do this anyway, but for the majority of developers managing these expirations can grow tedious.</span></span>

<span data-ttu-id="6a305-107">패키지 대상 우리의 개발자에 대 한 더 쉽게 확인 하려면 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) 설정 시간이 지나면 자동으로 만료 되는 페이로드를 만들기 위한 유틸리티 Api를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-107">To make this easier for our developer audience, the package [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) contains utility APIs for creating payloads that automatically expire after a set period of time.</span></span> <span data-ttu-id="6a305-108">이러한 Api의 오프 중지는 `ITimeLimitedDataProtector` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-108">These APIs hang off of the `ITimeLimitedDataProtector` type.</span></span>

## <a name="api-usage"></a><span data-ttu-id="6a305-109">API 사용</span><span class="sxs-lookup"><span data-stu-id="6a305-109">API usage</span></span>

<span data-ttu-id="6a305-110">`ITimeLimitedDataProtector` 인터페이스는 보호 하 고, 시간이 제한 된 / 자동으로 만료 되는 페이로드를 보호 해제에 대 한 핵심 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-110">The `ITimeLimitedDataProtector` interface is the core interface for protecting and unprotecting time-limited / self-expiring payloads.</span></span> <span data-ttu-id="6a305-111">인스턴스를 만드는 `ITimeLimitedDataProtector`, 일반의 인스턴스를 먼저 해야 [IDataProtector](overview.md) 특정 용도 사용 하 여 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-111">To create an instance of an `ITimeLimitedDataProtector`, you'll first need an instance of a regular [IDataProtector](overview.md) constructed with a specific purpose.</span></span> <span data-ttu-id="6a305-112">한 번의 `IDataProtector` 인스턴스를 사용할 수 있는 호출에서 `IDataProtector.ToTimeLimitedDataProtector` 기본 만료 기능 다시 보호기를 가져올 확장 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-112">Once the `IDataProtector` instance is available, call the `IDataProtector.ToTimeLimitedDataProtector` extension method to get back a protector with built-in expiration capabilities.</span></span>

<span data-ttu-id="6a305-113">`ITimeLimitedDataProtector`다음과 같은 API 화면 및 확장 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-113">`ITimeLimitedDataProtector` exposes the following API surface and extension methods:</span></span>

* <span data-ttu-id="6a305-114">CreateProtector (문자열 용도): ITimeLimitedDataProtector-이 API는 기존 비슷합니다 `IDataProtectionProvider.CreateProtector` 만들기를 사용할 수 있다는 점에서 [체인의 용도 위해](purpose-strings.md) 루트 시간이 제한 된 보호기를 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-114">CreateProtector(string purpose) : ITimeLimitedDataProtector - This API is similar to the existing `IDataProtectionProvider.CreateProtector` in that it can be used to create [purpose chains](purpose-strings.md) from a root time-limited protector.</span></span>

* <span data-ttu-id="6a305-115">Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]</span><span class="sxs-lookup"><span data-stu-id="6a305-115">Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="6a305-116">Protect(byte[] plaintext, TimeSpan lifetime) : byte[]</span><span class="sxs-lookup"><span data-stu-id="6a305-116">Protect(byte[] plaintext, TimeSpan lifetime) : byte[]</span></span>

* <span data-ttu-id="6a305-117">(바이트 일반 텍스트)를 보호: byte</span><span class="sxs-lookup"><span data-stu-id="6a305-117">Protect(byte[] plaintext) : byte[]</span></span>

* <span data-ttu-id="6a305-118">(문자열 일반 텍스트, DateTimeOffset 만료) 보호: 문자열</span><span class="sxs-lookup"><span data-stu-id="6a305-118">Protect(string plaintext, DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="6a305-119">보호 (문자열 일반 텍스트, TimeSpan 수명): 문자열</span><span class="sxs-lookup"><span data-stu-id="6a305-119">Protect(string plaintext, TimeSpan lifetime) : string</span></span>

* <span data-ttu-id="6a305-120">(문자열 일반 텍스트)를 보호: 문자열</span><span class="sxs-lookup"><span data-stu-id="6a305-120">Protect(string plaintext) : string</span></span>

<span data-ttu-id="6a305-121">핵심 외에도 `Protect` 의 일반 텍스트만 수행 하는 메서드는 페이로드의 만료 날짜를 지정할 수 있는 새로운 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-121">In addition to the core `Protect` methods which take only the plaintext, there are new overloads which allow specifying the payload's expiration date.</span></span> <span data-ttu-id="6a305-122">만료 날짜는 절대 날짜로 지정할 수 있습니다 (통해는 `DateTimeOffset`) 또는 상대 시간 (현재 시스템에서 시간을 통해는 `TimeSpan`).</span><span class="sxs-lookup"><span data-stu-id="6a305-122">The expiration date can be specified as an absolute date (via a `DateTimeOffset`) or as a relative time (from the current system time, via a `TimeSpan`).</span></span> <span data-ttu-id="6a305-123">만료 날짜를 사용 하지 않습니다는 오버 로드를 호출 하면 페이로드 가정 하지 만료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-123">If an overload which doesn't take an expiration is called, the payload is assumed never to expire.</span></span>

* <span data-ttu-id="6a305-124">Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]</span><span class="sxs-lookup"><span data-stu-id="6a305-124">Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="6a305-125">Unprotect(byte[] protectedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="6a305-125">Unprotect(byte[] protectedData) : byte[]</span></span>

* <span data-ttu-id="6a305-126">(DateTimeOffset 만료 아웃 문자열 protectedData)를 보호 해제: 문자열</span><span class="sxs-lookup"><span data-stu-id="6a305-126">Unprotect(string protectedData, out DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="6a305-127">(문자열 protectedData)를 보호 해제: 문자열</span><span class="sxs-lookup"><span data-stu-id="6a305-127">Unprotect(string protectedData) : string</span></span>

<span data-ttu-id="6a305-128">`Unprotect` 메서드 원래 보호 되지 않는 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-128">The `Unprotect` methods return the original unprotected data.</span></span> <span data-ttu-id="6a305-129">페이로드 아직 만료 되지 않았는지, 절대 만료를 선택적 출력 매개 변수는 원래 보호 되지 않는 데이터와 함께 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-129">If the payload hasn't yet expired, the absolute expiration is returned as an optional out parameter along with the original unprotected data.</span></span> <span data-ttu-id="6a305-130">페이로드 만료 되 면 CryptographicException Unprotect 메서드의 모든 오버 로드에 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-130">If the payload is expired, all overloads of the Unprotect method will throw CryptographicException.</span></span>

>[!WARNING]
> <span data-ttu-id="6a305-131">장기 또는 무기한 보존 해야 하는 페이로드를 보호 하기 위해 이러한 Api를 사용 하는 권장 되지 않습니다. 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-131">It's not advised to use these APIs to protect payloads which require long-term or indefinite persistence.</span></span> <span data-ttu-id="6a305-132">"있습니까 여유가 한 달이 지난 후 영구적으로 복구할 수 없게 하려면 보호 된 페이로드"?</span><span class="sxs-lookup"><span data-stu-id="6a305-132">"Can I afford for the protected payloads to be permanently unrecoverable after a month?"</span></span> <span data-ttu-id="6a305-133">바람직한 방법은;으로 사용할 수 있습니다. 대답 한 경우 다음 없습니다 개발자 대체 Api를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-133">can serve as a good rule of thumb; if the answer is no then developers should consider alternative APIs.</span></span>

<span data-ttu-id="6a305-134">사용 하 여 아래 샘플은 [DI 아닌 코드 경로](../configuration/non-di-scenarios.md) 데이터 보호 시스템을 인스턴스화하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-134">The sample below uses the [non-DI code paths](../configuration/non-di-scenarios.md) for instantiating the data protection system.</span></span> <span data-ttu-id="6a305-135">이 샘플을 실행 하려면 먼저 Microsoft.AspNetCore.DataProtection.Extensions 패키지에 대 한 참조를 추가 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a305-135">To run this sample, ensure that you have first added a reference to the Microsoft.AspNetCore.DataProtection.Extensions package.</span></span>

[!code-csharp[Main](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]
