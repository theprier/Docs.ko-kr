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
ms.openlocfilehash: 8b42e65bb6121355120a6f4fbe8cd4d1fea153de
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="e2aad-104">ASP.NET Core에서 데이터 보호: 소비자 API, 구성, 확장성 API 및 구현</span><span class="sxs-lookup"><span data-stu-id="e2aad-104">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="e2aad-105">데이터 보호 소개</span><span class="sxs-lookup"><span data-stu-id="e2aad-105">Introduction to Data Protection</span></span>](introduction.md)

* [<span data-ttu-id="e2aad-106">데이터 보호 API 시작</span><span class="sxs-lookup"><span data-stu-id="e2aad-106">Getting Started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="e2aad-107">소비자 API</span><span class="sxs-lookup"><span data-stu-id="e2aad-107">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="e2aad-108">소비자 API 개요</span><span class="sxs-lookup"><span data-stu-id="e2aad-108">Consumer APIs Overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="e2aad-109">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="e2aad-109">Purpose Strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="e2aad-110">용도 계층 구조 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="e2aad-110">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="e2aad-111">암호 해시</span><span class="sxs-lookup"><span data-stu-id="e2aad-111">Password Hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="e2aad-112">보호된 페이로드의 수명 제한</span><span class="sxs-lookup"><span data-stu-id="e2aad-112">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="e2aad-113">호출된 키가 속한 페이로드 보호 해제</span><span class="sxs-lookup"><span data-stu-id="e2aad-113">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="e2aad-114">구성</span><span class="sxs-lookup"><span data-stu-id="e2aad-114">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="e2aad-115">데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="e2aad-115">Configuring Data Protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="e2aad-116">기본 설정</span><span class="sxs-lookup"><span data-stu-id="e2aad-116">Default Settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="e2aad-117">컴퓨터 수준 정책</span><span class="sxs-lookup"><span data-stu-id="e2aad-117">Machine Wide Policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="e2aad-118">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="e2aad-118">Non DI Aware Scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="e2aad-119">확장성 API</span><span class="sxs-lookup"><span data-stu-id="e2aad-119">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="e2aad-120">Core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="e2aad-120">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="e2aad-121">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="e2aad-121">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="e2aad-122">기타 API</span><span class="sxs-lookup"><span data-stu-id="e2aad-122">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="e2aad-123">구현</span><span class="sxs-lookup"><span data-stu-id="e2aad-123">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="e2aad-124">인증된 암호화 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e2aad-124">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="e2aad-125">하위 키 파생 및 인증된 암호화</span><span class="sxs-lookup"><span data-stu-id="e2aad-125">Subkey Derivation and Authenticated Encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="e2aad-126">컨텍스트 헤더</span><span class="sxs-lookup"><span data-stu-id="e2aad-126">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="e2aad-127">키 관리</span><span class="sxs-lookup"><span data-stu-id="e2aad-127">Key Management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="e2aad-128">키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="e2aad-128">Key Storage Providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="e2aad-129">미사용 키 암호화</span><span class="sxs-lookup"><span data-stu-id="e2aad-129">Key Encryption At Rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="e2aad-130">키 불변성 및 설정 변경</span><span class="sxs-lookup"><span data-stu-id="e2aad-130">Key Immutability and Changing Settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="e2aad-131">키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="e2aad-131">Key Storage Format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="e2aad-132">삭제되는 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="e2aad-132">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="e2aad-133">호환성</span><span class="sxs-lookup"><span data-stu-id="e2aad-133">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="e2aad-134">응용프로그램 쿠키 공유</span><span class="sxs-lookup"><span data-stu-id="e2aad-134">Sharing cookies between applications</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="e2aad-135">ASP.NET에서 <machineKey> 바꾸기</span><span class="sxs-lookup"><span data-stu-id="e2aad-135">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
