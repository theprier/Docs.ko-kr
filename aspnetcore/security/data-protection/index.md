---
title: "ASP.NET Core에서 데이터 보호"
author: rick-anderson
description: "이 문서는 다양한 ASP.NET Core 데이터 보호 항목에 대한 목차로 사용됩니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/index
ms.openlocfilehash: 7bbd203a67b32032ba2ab82448a5fc9a495b52aa
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="d7aa2-103">ASP.NET Core에서 데이터 보호: 소비자 API, 구성, 확장성 API 및 구현</span><span class="sxs-lookup"><span data-stu-id="d7aa2-103">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="d7aa2-104">데이터 보호 소개</span><span class="sxs-lookup"><span data-stu-id="d7aa2-104">Introduction to data protection</span></span>](introduction.md)

* [<span data-ttu-id="d7aa2-105">데이터 보호 API 시작</span><span class="sxs-lookup"><span data-stu-id="d7aa2-105">Get started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="d7aa2-106">소비자 API</span><span class="sxs-lookup"><span data-stu-id="d7aa2-106">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="d7aa2-107">소비자 API 개요</span><span class="sxs-lookup"><span data-stu-id="d7aa2-107">Consumer APIs overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="d7aa2-108">용도 문자열</span><span class="sxs-lookup"><span data-stu-id="d7aa2-108">Purpose strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="d7aa2-109">용도 계층 구조 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="d7aa2-109">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="d7aa2-110">암호 해시</span><span class="sxs-lookup"><span data-stu-id="d7aa2-110">Password hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="d7aa2-111">보호된 페이로드의 수명 제한</span><span class="sxs-lookup"><span data-stu-id="d7aa2-111">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="d7aa2-112">호출된 키가 속한 페이로드 보호 해제</span><span class="sxs-lookup"><span data-stu-id="d7aa2-112">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="d7aa2-113">구성</span><span class="sxs-lookup"><span data-stu-id="d7aa2-113">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="d7aa2-114">데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="d7aa2-114">Configuring data protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="d7aa2-115">기본 설정</span><span class="sxs-lookup"><span data-stu-id="d7aa2-115">Default settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="d7aa2-116">컴퓨터 수준의 정책</span><span class="sxs-lookup"><span data-stu-id="d7aa2-116">Machine-wide policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="d7aa2-117">비 DI 인식 시나리오</span><span class="sxs-lookup"><span data-stu-id="d7aa2-117">Non DI-aware scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="d7aa2-118">확장성 API</span><span class="sxs-lookup"><span data-stu-id="d7aa2-118">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="d7aa2-119">Core 암호화 확장성</span><span class="sxs-lookup"><span data-stu-id="d7aa2-119">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="d7aa2-120">키 관리 확장성</span><span class="sxs-lookup"><span data-stu-id="d7aa2-120">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="d7aa2-121">기타 API</span><span class="sxs-lookup"><span data-stu-id="d7aa2-121">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="d7aa2-122">구현</span><span class="sxs-lookup"><span data-stu-id="d7aa2-122">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="d7aa2-123">인증된 암호화 세부 정보</span><span class="sxs-lookup"><span data-stu-id="d7aa2-123">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="d7aa2-124">하위 키 파생 및 인증된 암호화</span><span class="sxs-lookup"><span data-stu-id="d7aa2-124">Subkey derivation and authenticated encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="d7aa2-125">컨텍스트 헤더</span><span class="sxs-lookup"><span data-stu-id="d7aa2-125">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="d7aa2-126">키 관리</span><span class="sxs-lookup"><span data-stu-id="d7aa2-126">Key management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="d7aa2-127">키 저장소 공급자</span><span class="sxs-lookup"><span data-stu-id="d7aa2-127">Key storage providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="d7aa2-128">미사용 키 암호화</span><span class="sxs-lookup"><span data-stu-id="d7aa2-128">Key encryption at rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="d7aa2-129">키 불변성 및 설정 변경</span><span class="sxs-lookup"><span data-stu-id="d7aa2-129">Key immutability and changing settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="d7aa2-130">키 저장소 형식</span><span class="sxs-lookup"><span data-stu-id="d7aa2-130">Key storage format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="d7aa2-131">삭제되는 데이터 보호 공급자</span><span class="sxs-lookup"><span data-stu-id="d7aa2-131">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="d7aa2-132">호환성</span><span class="sxs-lookup"><span data-stu-id="d7aa2-132">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="d7aa2-133">앱 간에 쿠키 공유</span><span class="sxs-lookup"><span data-stu-id="d7aa2-133">Sharing cookies between apps</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="d7aa2-134">ASP.NET에서 <machineKey> 바꾸기</span><span class="sxs-lookup"><span data-stu-id="d7aa2-134">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
