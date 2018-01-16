---
title: "ASP.NET Core에서 데이터 보호"
author: rick-anderson
description: "이 문서는 다양한 ASP.NET Core 데이터 보호 항목에 대한 목차로 사용됩니다."
keywords: "ASP.NET Core,데이터 보호"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 1f402da8-1052-4970-9835-9f9f16a02dbc
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/index
ms.openlocfilehash: cbf18c6ec867fefec22980f3e3493562594ef72d
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="51c95-104">ASP.NET Core에서 데이터 보호: 소비자 API, 구성, 확장성 API 및 구현</span><span class="sxs-lookup"><span data-stu-id="51c95-104">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="51c95-105">데이터 보호 소개</span><span class="sxs-lookup"><span data-stu-id="51c95-105">Introduction to data protection</span></span>](introduction.md)

* [<span data-ttu-id="51c95-106">데이터 보호 API 시작</span><span class="sxs-lookup"><span data-stu-id="51c95-106">Get started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="51c95-107">소비자 API</span><span class="sxs-lookup"><span data-stu-id="51c95-107">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="51c95-108">소비자 API 개요</span><span class="sxs-lookup"><span data-stu-id="51c95-108">Consumer APIs overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="51c95-109">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="51c95-109">Purpose strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="51c95-110">용도 계층 구조 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="51c95-110">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="51c95-111">암호 해시</span><span class="sxs-lookup"><span data-stu-id="51c95-111">Password hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="51c95-112">보호된 페이로드의 수명 제한</span><span class="sxs-lookup"><span data-stu-id="51c95-112">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="51c95-113">호출된 키가 속한 페이로드 보호 해제</span><span class="sxs-lookup"><span data-stu-id="51c95-113">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="51c95-114">구성</span><span class="sxs-lookup"><span data-stu-id="51c95-114">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="51c95-115">데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="51c95-115">Configuring data protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="51c95-116">기본 설정</span><span class="sxs-lookup"><span data-stu-id="51c95-116">Default settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="51c95-117">컴퓨터 수준의 정책</span><span class="sxs-lookup"><span data-stu-id="51c95-117">Machine-wide policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="51c95-118">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="51c95-118">Non DI-aware scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="51c95-119">확장성 API</span><span class="sxs-lookup"><span data-stu-id="51c95-119">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="51c95-120">Core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="51c95-120">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="51c95-121">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="51c95-121">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="51c95-122">기타 API</span><span class="sxs-lookup"><span data-stu-id="51c95-122">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="51c95-123">구현</span><span class="sxs-lookup"><span data-stu-id="51c95-123">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="51c95-124">인증된 암호화 세부 정보</span><span class="sxs-lookup"><span data-stu-id="51c95-124">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="51c95-125">하위 키 파생 및 인증된 암호화</span><span class="sxs-lookup"><span data-stu-id="51c95-125">Subkey derivation and authenticated encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="51c95-126">컨텍스트 헤더</span><span class="sxs-lookup"><span data-stu-id="51c95-126">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="51c95-127">키 관리</span><span class="sxs-lookup"><span data-stu-id="51c95-127">Key management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="51c95-128">키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="51c95-128">Key storage providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="51c95-129">미사용 키 암호화</span><span class="sxs-lookup"><span data-stu-id="51c95-129">Key encryption at rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="51c95-130">키 불변성 및 설정 변경</span><span class="sxs-lookup"><span data-stu-id="51c95-130">Key immutability and changing settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="51c95-131">키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="51c95-131">Key storage format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="51c95-132">삭제되는 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="51c95-132">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="51c95-133">호환성</span><span class="sxs-lookup"><span data-stu-id="51c95-133">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="51c95-134">앱 간에 쿠키 공유</span><span class="sxs-lookup"><span data-stu-id="51c95-134">Sharing cookies between apps</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="51c95-135">ASP.NET에서 <machineKey> 바꾸기</span><span class="sxs-lookup"><span data-stu-id="51c95-135">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
