---
title: ASP.NET Core에서 데이터 보호
author: rick-anderson
description: 이 문서는 다양한 ASP.NET Core 데이터 보호 항목에 대한 목차로 사용됩니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/index
ms.openlocfilehash: 83b5bb1e6a4942a4d3e5ec0d445fa6e5a21fb533
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30071698"
---
# <a name="data-protection-in-aspnet-core"></a><span data-ttu-id="ba690-103">ASP.NET Core에서 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="ba690-103">Data Protection in ASP.NET Core</span></span>

* [<span data-ttu-id="ba690-104">데이터 보호 소개</span><span class="sxs-lookup"><span data-stu-id="ba690-104">Introduction to data protection</span></span>](xref:security/data-protection/introduction)

* [<span data-ttu-id="ba690-105">데이터 보호 API 시작</span><span class="sxs-lookup"><span data-stu-id="ba690-105">Get started with the Data Protection APIs</span></span>](xref:security/data-protection/using-data-protection)

* [<span data-ttu-id="ba690-106">소비자 API</span><span class="sxs-lookup"><span data-stu-id="ba690-106">Consumer APIs</span></span>](xref:security/data-protection/consumer-apis/index)

  * [<span data-ttu-id="ba690-107">소비자 API 개요</span><span class="sxs-lookup"><span data-stu-id="ba690-107">Consumer APIs overview</span></span>](xref:security/data-protection/consumer-apis/overview)

  * [<span data-ttu-id="ba690-108">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="ba690-108">Purpose strings</span></span>](xref:security/data-protection/consumer-apis/purpose-strings)

  * [<span data-ttu-id="ba690-109">용도 계층 구조 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="ba690-109">Purpose hierarchy and multi-tenancy</span></span>](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [<span data-ttu-id="ba690-110">해시 암호</span><span class="sxs-lookup"><span data-stu-id="ba690-110">Hash passwords</span></span>](xref:security/data-protection/consumer-apis/password-hashing)

  * [<span data-ttu-id="ba690-111">보호된 페이로드의 수명 제한</span><span class="sxs-lookup"><span data-stu-id="ba690-111">Limit the lifetime of protected payloads</span></span>](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [<span data-ttu-id="ba690-112">호출된 키가 속한 페이로드 보호 해제</span><span class="sxs-lookup"><span data-stu-id="ba690-112">Unprotect payloads whose keys have been revoked</span></span>](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [<span data-ttu-id="ba690-113">구성</span><span class="sxs-lookup"><span data-stu-id="ba690-113">Configuration</span></span>](xref:security/data-protection/configuration/index)

  * [<span data-ttu-id="ba690-114">ASP.NET Core 데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="ba690-114">Configure ASP.NET Core Data Protection</span></span>](xref:security/data-protection/configuration/overview)

  * [<span data-ttu-id="ba690-115">기본 설정</span><span class="sxs-lookup"><span data-stu-id="ba690-115">Default settings</span></span>](xref:security/data-protection/configuration/default-settings)

  * [<span data-ttu-id="ba690-116">컴퓨터 수준의 정책</span><span class="sxs-lookup"><span data-stu-id="ba690-116">Machine-wide policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)

  * [<span data-ttu-id="ba690-117">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="ba690-117">Non DI-aware scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)

* [<span data-ttu-id="ba690-118">확장성 API</span><span class="sxs-lookup"><span data-stu-id="ba690-118">Extensibility APIs</span></span>](xref:security/data-protection/extensibility/index)

  * [<span data-ttu-id="ba690-119">Core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="ba690-119">Core cryptography extensibility</span></span>](xref:security/data-protection/extensibility/core-crypto)

  * [<span data-ttu-id="ba690-120">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="ba690-120">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)

  * [<span data-ttu-id="ba690-121">기타 API</span><span class="sxs-lookup"><span data-stu-id="ba690-121">Miscellaneous APIs</span></span>](xref:security/data-protection/extensibility/misc-apis)

* [<span data-ttu-id="ba690-122">구현</span><span class="sxs-lookup"><span data-stu-id="ba690-122">Implementation</span></span>](xref:security/data-protection/implementation/index)

  * [<span data-ttu-id="ba690-123">인증된 암호화 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ba690-123">Authenticated encryption details</span></span>](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [<span data-ttu-id="ba690-124">하위 키 파생 및 인증된 암호화</span><span class="sxs-lookup"><span data-stu-id="ba690-124">Subkey derivation and authenticated encryption</span></span>](xref:security/data-protection/implementation/subkeyderivation)

  * [<span data-ttu-id="ba690-125">컨텍스트 헤더</span><span class="sxs-lookup"><span data-stu-id="ba690-125">Context headers</span></span>](xref:security/data-protection/implementation/context-headers)

  * [<span data-ttu-id="ba690-126">키 관리</span><span class="sxs-lookup"><span data-stu-id="ba690-126">Key management</span></span>](xref:security/data-protection/implementation/key-management)

  * [<span data-ttu-id="ba690-127">키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="ba690-127">Key storage providers</span></span>](xref:security/data-protection/implementation/key-storage-providers)

  * [<span data-ttu-id="ba690-128">미사용 키 암호화</span><span class="sxs-lookup"><span data-stu-id="ba690-128">Key encryption at rest</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [<span data-ttu-id="ba690-129">키 불변성 및 설정</span><span class="sxs-lookup"><span data-stu-id="ba690-129">Key immutability and settings</span></span>](xref:security/data-protection/implementation/key-immutability)

  * [<span data-ttu-id="ba690-130">키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="ba690-130">Key storage format</span></span>](xref:security/data-protection/implementation/key-storage-format)

  * [<span data-ttu-id="ba690-131">삭제되는 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="ba690-131">Ephemeral data protection providers</span></span>](xref:security/data-protection/implementation/key-storage-ephemeral)

* [<span data-ttu-id="ba690-132">호환성</span><span class="sxs-lookup"><span data-stu-id="ba690-132">Compatibility</span></span>](xref:security/data-protection/compatibility/index)

  * [<span data-ttu-id="ba690-133">ASP.NET Core에서 ASP.NET <machineKey> 교체</span><span class="sxs-lookup"><span data-stu-id="ba690-133">Replacing ASP.NET <machineKey> in ASP.NET Core</span></span>](xref:security/data-protection/compatibility/replacing-machinekey)
