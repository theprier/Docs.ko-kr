---
title: "용도 문자열"
author: rick-anderson
description: "이 문서의 목적은 문자열 ASP.NET Core 데이터 보호 Api에서에서 사용 되는 방법을 자세히 설명 합니다."
keywords: "ASP.NET Core, 데이터 보호, 목적 문자열"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: c96ed361-c382-4980-8933-800e740cfc38
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/purpose-strings
ms.openlocfilehash: 0d759937703d2a25604042b5e74e71155d635c1b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="purpose-strings"></a><span data-ttu-id="013b2-104">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="013b2-104">Purpose Strings</span></span>

<a name="data-protection-consumer-apis-purposes"></a>

<span data-ttu-id="013b2-105">사용 하는 구성 요소 `IDataProtectionProvider` 고유한 전달 해야 *목적으로* 매개 변수를는 `CreateProtector` 메서드.</span><span class="sxs-lookup"><span data-stu-id="013b2-105">Components which consume `IDataProtectionProvider` must pass a unique *purposes* parameter to the `CreateProtector` method.</span></span> <span data-ttu-id="013b2-106">목적 *매개 변수* 루트 암호화 키가 동일한 경우에 암호화 소비자 간에 격리 제공 하므로 보안에는 데이터 보호 시스템에 대 한 내재 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-106">The purposes *parameter* is inherent to the security of the data protection system, as it provides isolation between cryptographic consumers, even if the root cryptographic keys are the same.</span></span>

<span data-ttu-id="013b2-107">소비자는 용도 지정 하는 경우에 해당 고객에 게 고유 암호화 하위 키를 파생 시키는 목적 문자열이 루트 암호화 키와 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-107">When a consumer specifies a purpose, the purpose string is used along with the root cryptographic keys to derive cryptographic subkeys unique to that consumer.</span></span> <span data-ttu-id="013b2-108">응용 프로그램에서 다른 모든 암호화 소비자에 게 소비자 그래야만: 다른 구성 요소가 없으면 해당 페이로드를 읽을 수 있으며 모든 다른 구성 요소의 페이로드를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-108">This isolates the consumer from all other cryptographic consumers in the application: no other component can read its payloads, and it cannot read any other component's payloads.</span></span> <span data-ttu-id="013b2-109">이 격리는 또한 부적합 모든 범주의 구성 요소에 대 한 공격을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-109">This isolation also renders infeasible entire categories of attack against the component.</span></span>

![용도 다이어그램 예제](purpose-strings/_static/purposes.png)

<span data-ttu-id="013b2-111">위의 다이어그램에서 `IDataProtector` 인스턴스 A와 B **없습니다** 페이로드를 읽을 서로의만 자신의 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-111">In the diagram above, `IDataProtector` instances A and B **cannot** read each other's payloads, only their own.</span></span>

<span data-ttu-id="013b2-112">용도 문자열 본인 확인 될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-112">The purpose string doesn't have to be secret.</span></span> <span data-ttu-id="013b2-113">단순히 다른 올바르게 동작 구성 요소가 없으면 동일한 목적 문자열로 제공 적이 됩니다 의미에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-113">It should simply be unique in the sense that no other well-behaved component will ever provide the same purpose string.</span></span>

>[!TIP]
> <span data-ttu-id="013b2-114">데이터 보호 Api를 사용 하는 구성 요소의 네임 스페이스 및 형식 이름을 사용 하는 좋은 경험상, 연습이 정보를 충돌 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-114">Using the namespace and type name of the component consuming the data protection APIs is a good rule of thumb, as in practice this information will never conflict.</span></span>
>
><span data-ttu-id="013b2-115">전달자 토큰 minting 담당 하는 Contoso에서 작성 된 구성 요소는 해당 용도 문자열로 Contoso.Security.BearerToken을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-115">A Contoso-authored component which is responsible for minting bearer tokens might use Contoso.Security.BearerToken as its purpose string.</span></span> <span data-ttu-id="013b2-116">또는-더 좋은-Contoso.Security.BearerToken.v1의 목적은 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-116">Or - even better - it might use Contoso.Security.BearerToken.v1 as its purpose string.</span></span> <span data-ttu-id="013b2-117">Contoso.Security.BearerToken.v2의 목적으로 사용 하도록 이후 버전을 사용 하면 버전 번호를 추가 하 고 페이로드 이동 관련해 서 다양 한 버전 서로 완전히 격리는 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-117">Appending the version number allows a future version to use Contoso.Security.BearerToken.v2 as its purpose, and the different versions would be completely isolated from one another as far as payloads go.</span></span>

<span data-ttu-id="013b2-118">목적으로 매개 변수를 이후 `CreateProtector` 문자열 배열에는 위의 수 대신로 지정 되어 있지 `[ "Contoso.Security.BearerToken", "v1" ]`합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-118">Since the purposes parameter to `CreateProtector` is a string array, the above could have been instead specified as `[ "Contoso.Security.BearerToken", "v1" ]`.</span></span> <span data-ttu-id="013b2-119">이 목적으로 계층 구조 설정를 통해 데이터 보호 시스템을 사용 하는 다중 테 넌 트 시나리오의 가능성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-119">This allows establishing a hierarchy of purposes and opens up the possibility of multi-tenancy scenarios with the data protection system.</span></span>

<a name="data-protection-contoso-purpose"></a>

>[!WARNING]
> <span data-ttu-id="013b2-120">구성 요소에서 신뢰할 수 없는 사용자 입력을 위해 체인에 대 한 입력의 유일한 출처로 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-120">Components should not allow untrusted user input to be the sole source of input for the purposes chain.</span></span>
>
><span data-ttu-id="013b2-121">예를 들어 구성 요소를 Contoso.Messaging.SecureMessage 보안 메시지를 저장 하기 위한 담당 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-121">For example, consider a component Contoso.Messaging.SecureMessage which is responsible for storing secure messages.</span></span> <span data-ttu-id="013b2-122">보안 메시징 구성 요소를 호출할 경우 `CreateProtector([ username ])`, 악의적인 사용자가을 호출 하는 구성 요소를 가져오지를 username "Contoso.Security.BearerToken" 계정에 만들 수 있습니다 다음 `CreateProtector([ "Contoso.Security.BearerToken" ])`, 실수로 인해 보안 메시징 인증 토큰으로 인식 mint 페이로드를 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-122">If the secure messaging component were to call `CreateProtector([ username ])`, then a malicious user might create an account with username "Contoso.Security.BearerToken" in an attempt to get the component to call `CreateProtector([ "Contoso.Security.BearerToken" ])`, thus inadvertently causing the secure messaging system to mint payloads that could be perceived as authentication tokens.</span></span>
>
><span data-ttu-id="013b2-123">메시징 구성 요소에 대 한 더 나은 목적으로 체인 것 `CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])`, 적절 한 격리를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-123">A better purposes chain for the messaging component would be `CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])`, which provides proper isolation.</span></span>

<span data-ttu-id="013b2-124">동작 및에서 제공 되는 격리 `IDataProtectionProvider`, `IDataProtector`, 및 용도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-124">The isolation provided by and behaviors of `IDataProtectionProvider`, `IDataProtector`, and purposes are as follows:</span></span>

* <span data-ttu-id="013b2-125">에 대 한는 주어진 `IDataProtectionProvider` 개체는 `CreateProtector` 메서드 만듭니다는 `IDataProtector` 둘 다에 고유 하 게 연결 된 개체는 `IDataProtectionProvider` 은 목적으로 매개 변수를 메서드에 전달 된를 만든 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-125">For a given `IDataProtectionProvider` object, the `CreateProtector` method will create an `IDataProtector` object uniquely tied to both the `IDataProtectionProvider` object which created it and the purposes parameter which was passed into the method.</span></span>

* <span data-ttu-id="013b2-126">용도 매개 변수가 null 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-126">The purpose parameter must not be null.</span></span> <span data-ttu-id="013b2-127">(목적으로 배열로 지정 된 경우 즉, 배열의 길이가 0 인 되지 않아야 하 고 배열의 모든 요소는 null 이어야 합니다.) 빈 문자열 목적 기술적으로 사용할 수 있지만 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-127">(If purposes is specified as an array, this means that the array must not be of zero length and all elements of the array must be non-null.) An empty string purpose is technically allowed but is discouraged.</span></span>

* <span data-ttu-id="013b2-128">두 가지 목적으로 인수는 동일한 순서로 동일한 문자열 (서 수는 비교자를 사용 하 여)를 포함 하는 경우에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-128">Two purposes arguments are equivalent if and only if they contain the same strings (using an ordinal comparer) in the same order.</span></span> <span data-ttu-id="013b2-129">단일 용도 인수 해당 단일 요소 목적으로 배열 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-129">A single purpose argument is equivalent to the corresponding single-element purposes array.</span></span>

* <span data-ttu-id="013b2-130">두 개의 `IDataProtector` 해당에서 만들어진 경우에 개체가 동일한 지 `IDataProtectionProvider` 해당 목적으로 매개 변수를 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-130">Two `IDataProtector` objects are equivalent if and only if they are created from equivalent `IDataProtectionProvider` objects with equivalent purposes parameters.</span></span>

* <span data-ttu-id="013b2-131">에 대 한는 주어진 `IDataProtector` 개체에 대 한 호출 `Unprotect(protectedData)` 는 원래 반환 `unprotectedData` 경우에 `protectedData := Protect(unprotectedData)` 해당 `IDataProtector` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-131">For a given `IDataProtector` object, a call to `Unprotect(protectedData)` will return the original `unprotectedData` if and only if `protectedData := Protect(unprotectedData)` for an equivalent `IDataProtector` object.</span></span>

> [!NOTE]
> <span data-ttu-id="013b2-132">다른 구성 요소와 충돌 하는 목적은 문자열에 일부 구성 요소 의도적으로 선택 하는 경우를 하려고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-132">We're not considering the case where some component intentionally chooses a purpose string which is known to conflict with another component.</span></span> <span data-ttu-id="013b2-133">이러한 구성 요소는 기본적으로 간주 되 악성 하며이 시스템에 작업자 프로세스 내의 악성 코드가 이미 실행 되 고 보안 보장을 제공 하 없습니다.</span><span class="sxs-lookup"><span data-stu-id="013b2-133">Such a component would essentially be considered malicious, and this system is not intended to provide security guarantees in the event that malicious code is already running inside of the worker process.</span></span>
