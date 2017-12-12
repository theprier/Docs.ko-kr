---
title: "데이터 보호에 대 한 키 관리 및 ASP.NET Core 수명"
author: rick-anderson
description: "데이터 보호 키 관리 및 ASP.NET 코어의 수명에 알아봅니다."
keywords: "ASP.NET Core 키 관리, DPAPI, 데이터 보호 키 수명"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: ef7dad2a-7029-4ae5-8f06-1fbebedccaa4
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: 4f5409acf4d934ced828153ccfd945834d0f1718
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a><span data-ttu-id="974dd-104">데이터 보호에 대 한 키 관리 및 ASP.NET Core 수명</span><span class="sxs-lookup"><span data-stu-id="974dd-104">Data Protection key management and lifetime in ASP.NET Core</span></span>

<span data-ttu-id="974dd-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="974dd-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="key-management"></a><span data-ttu-id="974dd-106">키 관리</span><span class="sxs-lookup"><span data-stu-id="974dd-106">Key management</span></span>

<span data-ttu-id="974dd-107">응용 프로그램 운영 환경을 검색 하 고 자체적으로 키 구성 처리 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-107">The app attempts to detect its operational environment and handle key configuration on its own.</span></span>

1. <span data-ttu-id="974dd-108">응용 프로그램에서 호스트 될 경우 [Azure 앱](https://azure.microsoft.com/services/app-service/), 키에 저장 됩니다는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-108">If the app is hosted in [Azure Apps](https://azure.microsoft.com/services/app-service/), keys are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="974dd-109">이 폴더는 네트워크 저장소에서 지원 하 고 응용 프로그램을 호스트 하는 모든 컴퓨터에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-109">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span>
   * <span data-ttu-id="974dd-110">저장 된 상태의 키를 보호 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-110">Keys aren't protected at rest.</span></span>
   * <span data-ttu-id="974dd-111">*DataProtection 키* 폴더 키 링을 단일 배포 슬롯에서 응용 프로그램의 모든 인스턴스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-111">The *DataProtection-Keys* folder supplies the key ring to all instances of an app in a single deployment slot.</span></span>
   * <span data-ttu-id="974dd-112">스테이징 및 프로덕션, 같은 별도 배포 슬롯 키 링을 공유 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-112">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span> <span data-ttu-id="974dd-113">예를 들어 스테이징 및 프로덕션을 교체 하거나 A를 사용 하 여 배포 슬롯 간에 교환 / B 테스트, 모든 앱 데이터 보호를 사용 하 여 이전 슬롯 내 키 링을 사용 하 여 저장 된 데이터를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-113">When you swap between deployment slots, for example swapping Staging to Production or using A/B testing, any app using Data Protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="974dd-114">이 데이터 보호를 사용 하 여 쿠키를 보호 하기 위해 표준 ASP.NET Core 쿠키 인증을 사용 하는 응용 프로그램에서 기록 되 고 사용자에 게 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-114">This leads to users being logged out of an app that uses the standard ASP.NET Core cookie authentication, as it uses Data Protection to protect its cookies.</span></span> <span data-ttu-id="974dd-115">슬롯에 관계 없이 키 링을 원하는 경우 Azure Blob 저장소, Azure 주요 자격 증명 모음 SQL 저장소 등의 외부 키 링 공급자를 사용 하거나 Redis 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-115">If you desire slot-independent key rings, use an external key ring provider, such as Azure Blob Storage, Azure Key Vault, a SQL store, or Redis cache.</span></span>

1. <span data-ttu-id="974dd-116">키에 유지 되기 사용자 프로필을 사용할 수 있는 경우는 *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-116">If the user profile is available, keys are persisted to the *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="974dd-117">운영 체제가 Windows 인 경우 키 DPAPI를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-117">If the operating system is Windows, the keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="974dd-118">응용 프로그램을 IIS에서 호스트 하는 경우 키 하 게 포함 되었는지 작업자 프로세스 계정에만 있는 특별 한 레지스트리 키에서 HKLM 레지스트리 에서도 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-118">If the app is hosted in IIS, keys are persisted to the HKLM registry in a special registry key that is ACLed only to the worker process account.</span></span> <span data-ttu-id="974dd-119">미사용 키는 DPAPI를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-119">Keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="974dd-120">일치 이러한 조건 중 없을 경우 현재 프로세스 외부에서 키 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-120">If none of these conditions match, keys aren't persisted outside of the current process.</span></span> <span data-ttu-id="974dd-121">생성 된 모든 종료 프로세스가 종료 키 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-121">When the process shuts down, all generated keys are lost.</span></span>

<span data-ttu-id="974dd-122">개발자는 항상 모든 권한 및 키가 저장 하는 방법과 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-122">The developer is always in full control and can override how and where keys are stored.</span></span> <span data-ttu-id="974dd-123">위의 처음 세 옵션은 대부분의 응용 프로그램 방법과 유사 좋은 기본값을 제공 해야 ASP.NET  **\<machineKey >** 자동 생성 루틴 이전에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-123">The first three options above should provide good defaults for most apps similar to how the ASP.NET **\<machineKey>** auto-generation routines worked in the past.</span></span> <span data-ttu-id="974dd-124">최종, 대체 옵션은 개발자가 지정할 수 필요로 하는 유일한 시나리오 [구성](xref:security/data-protection/configuration/overview) 선행 키 지 속성을 원하는 하지만이 대체 (fallback이) 드문 경우에만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-124">The final, fallback option is the only scenario that requires the developer to specify [configuration](xref:security/data-protection/configuration/overview) upfront if they want key persistence, but this fallback only occurs in rare situations.</span></span>

<span data-ttu-id="974dd-125">Docker 볼륨 (공유 볼륨 또는 컨테이너의 수명이 지속 되 면 호스트 탑재 된 볼륨)가 있는 폴더에 키를 유지할지를 Docker 컨테이너에서 호스팅하는 경우 또는 외부 공급자와 같은 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 또는 [Redis](https://redis.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-125">When hosting in a Docker container, keys should be persisted in a folder that's a Docker volume (a shared volume or a host-mounted volume that persists beyond the container's lifetime) or in an external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span> <span data-ttu-id="974dd-126">앱 공유 네트워크 볼륨에 액세스할 수 없는 경우 외부 공급자 웹 팜 시나리오에 도움이 됩니다 (참조 [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) 자세한 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="974dd-126">An external provider is also useful in web farm scenarios if apps can't access a shared network volume (see [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) for more information).</span></span>

> [!WARNING]
> <span data-ttu-id="974dd-127">개발자는 위에 설명 된 규칙을 재정의 하 고 데이터 보호 시스템에 특정 키 저장소를 가리키는, 미사용 키의 자동 암호화는 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-127">If the developer overrides the rules outlined above and points the Data Protection system at a specific key repository, automatic encryption of keys at rest is disabled.</span></span> <span data-ttu-id="974dd-128">Rest에 보호를 통해 다시 사용 되도록 설정 될 수 있습니다 [구성](xref:security/data-protection/configuration/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-128">At-rest protection can be re-enabled via [configuration](xref:security/data-protection/configuration/overview).</span></span>

## <a name="key-lifetime"></a><span data-ttu-id="974dd-129">키 수명</span><span class="sxs-lookup"><span data-stu-id="974dd-129">Key lifetime</span></span>

<span data-ttu-id="974dd-130">키는은 기본적으로는 90 일 수명을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-130">Keys have a 90-day lifetime by default.</span></span> <span data-ttu-id="974dd-131">키 만료 되 면 응용 프로그램 자동으로 새 키를 생성 하 고 새 키를 활성 키로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-131">When a key expires, the app automatically generates a new key and sets the new key as the active key.</span></span> <span data-ttu-id="974dd-132">사용 중지 된 키를 시스템에 유지,으로 앱 사람과 보호 되는 모든 데이터를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-132">As long as retired keys remain on the system, your app can decrypt any data protected with them.</span></span> <span data-ttu-id="974dd-133">참조 [키 관리](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-133">See [key management](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) for more information.</span></span>

## <a name="default-algorithms"></a><span data-ttu-id="974dd-134">기본 알고리즘</span><span class="sxs-lookup"><span data-stu-id="974dd-134">Default algorithms</span></span>

<span data-ttu-id="974dd-135">기본 페이로드 보호 알고리즘 사용은 AES-256-CBC 기밀성 및 HMACSHA256에 대 한 신뢰성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-135">The default payload protection algorithm used is AES-256-CBC for confidentiality and HMACSHA256 for authenticity.</span></span> <span data-ttu-id="974dd-136">페이로드 당 별로 이러한 알고리즘에 사용 되는 두 개의 하위 키를 파생 90 일 마다 변경 512 비트 마스터 키가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-136">A 512-bit master key, changed every 90 days, is used to derive the two sub-keys used for these algorithms on a per-payload basis.</span></span> <span data-ttu-id="974dd-137">참조 [파생 하위](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="974dd-137">See [subkey derivation](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="974dd-138">참고 항목</span><span class="sxs-lookup"><span data-stu-id="974dd-138">See also</span></span>

* [<span data-ttu-id="974dd-139">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="974dd-139">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)
