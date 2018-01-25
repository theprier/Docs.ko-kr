---
title: "키 불변성 및 설정 변경"
author: rick-anderson
description: "이 문서에는 ASP.NET Core 데이터 보호 키 불변성 Api의 구현 세부 사항을 설명합니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-immutability
ms.openlocfilehash: 425b8ba9769c2b5ac635693b045e52c110f25205
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="key-immutability-and-changing-settings"></a><span data-ttu-id="73177-103">주요 불변성 및 설정 변경</span><span class="sxs-lookup"><span data-stu-id="73177-103">Key Immutability and changing settings</span></span>

<span data-ttu-id="73177-104">개체는 백업 저장소에 유지 되 면 표현 영원히 고정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73177-104">Once an object is persisted to the backing store, its representation is forever fixed.</span></span> <span data-ttu-id="73177-105">새 데이터에는 백업 저장소에 추가할 수 있지만 기존 데이터를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73177-105">New data can be added to the backing store, but existing data can never be mutated.</span></span> <span data-ttu-id="73177-106">이 동작의 주 목적은 데이터 손상을 방지 하려면입니다.</span><span class="sxs-lookup"><span data-stu-id="73177-106">The primary purpose of this behavior is to prevent data corruption.</span></span>

<span data-ttu-id="73177-107">이 동작의 한 결과 키를 백업 저장소에 쓴 후 아닌지 변경할 수는입니다.</span><span class="sxs-lookup"><span data-stu-id="73177-107">One consequence of this behavior is that once a key is written to the backing store, it's immutable.</span></span> <span data-ttu-id="73177-108">생성, 활성화 및 만료 날짜는 변경할 수 없습니다, 사용 하 여 취소할 수 있지만 `IKeyManager`합니다.</span><span class="sxs-lookup"><span data-stu-id="73177-108">Its creation, activation, and expiration dates can never be changed, though it can revoked by using `IKeyManager`.</span></span> <span data-ttu-id="73177-109">또한 해당 기본 알고리즘 정보, 마스터 키 자료 및 나머지 속성에서 암호화도 변경할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73177-109">Additionally, its underlying algorithmic information, master keying material, and encryption at rest properties are also immutable.</span></span>

<span data-ttu-id="73177-110">다음에 키를 생성 하기 위해 명시적 호출이 통해 될 때까지 해당 변경 내용이 반영 다루지는 않겠습니다. 개발자는 설정 키 지 속성에 영향을 주는 변경 되 면 `IKeyManager.CreateNewKey` 또는 데이터 보호 시스템의 자체를 통해 [자동 키 세대](key-management.md#data-protection-implementation-key-management) 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="73177-110">If the developer changes any setting that affects key persistence, those changes won't go into effect until the next time a key is generated, either via an explicit call to `IKeyManager.CreateNewKey` or via the data protection system's own [automatic key generation](key-management.md#data-protection-implementation-key-management) behavior.</span></span> <span data-ttu-id="73177-111">지 속성 키에 영향을 주는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73177-111">The settings that affect key persistence are as follows:</span></span>

* [<span data-ttu-id="73177-112">기본 키 수명</span><span class="sxs-lookup"><span data-stu-id="73177-112">The default key lifetime</span></span>](key-management.md#data-protection-implementation-key-management)

* [<span data-ttu-id="73177-113">나머지 메커니즘에 키 암호화</span><span class="sxs-lookup"><span data-stu-id="73177-113">The key encryption at rest mechanism</span></span>](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest)

* [<span data-ttu-id="73177-114">키 내에 포함 된 알고리즘 정보</span><span class="sxs-lookup"><span data-stu-id="73177-114">The algorithmic information contained within the key</span></span>](xref:security/data-protection/configuration/overview#changing-algorithms-with-usecryptographicalgorithms)

<span data-ttu-id="73177-115">이러한 설정은 다음 자동 키 롤링 시간 이전의 조정이 시작 해야 할 경우 만드는 것을 고려 하기 위해 명시적 호출이 `IKeyManager.CreateNewKey` 를 새 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73177-115">If you need these settings to kick in earlier than the next automatic key rolling time, consider making an explicit call to `IKeyManager.CreateNewKey` to force the creation of a new key.</span></span> <span data-ttu-id="73177-116">명시적으로 활성화 날짜를 제공 해야 합니다. ({이제 + 2 일을 (를)이는 바람직한 방법은 전파에 대 한 변경에 대 한 시간을 허용 하도록) 및 호출에 대 한 만료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="73177-116">Remember to provide an explicit activation date ({ now + 2 days } is a good rule of thumb to allow time for the change to propagate) and expiration date in the call.</span></span>

>[!TIP]
> <span data-ttu-id="73177-117">저장소를 변경 하는 모든 응용 프로그램에 사용 하 여 동일한 설정을 지정 해야는 `IDataProtectionBuilder` 확장 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="73177-117">All applications touching the repository should specify the same settings with the `IDataProtectionBuilder` extension methods.</span></span> <span data-ttu-id="73177-118">그렇지 않으면, 지속형된 키의 속성 키 생성 루틴을 호출 하는 특정 응용 프로그램에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73177-118">Otherwise, the properties of the persisted key will be dependent on the particular application that invoked the key generation routines.</span></span>
