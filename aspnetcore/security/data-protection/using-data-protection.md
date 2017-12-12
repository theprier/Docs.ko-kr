---
title: "데이터 보호 Api 시작"
author: rick-anderson
description: "이 문서에서는 보호 하 고, 응용 프로그램의 데이터를 보호 해제에 대 한 ASP.NET Core 데이터 보호 Api를 사용 하는 방법을 설명 합니다."
keywords: "ASP.NET Core, 데이터 보호"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 39b7a73c-29d4-4137-b311-49529adcf3cb
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/using-data-protection
ms.openlocfilehash: 535bfaf2077cda91c27e7d0d68b9804e8596070e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="getting-started-with-the-data-protection-apis"></a><span data-ttu-id="b7989-104">데이터 보호 Api 시작</span><span class="sxs-lookup"><span data-stu-id="b7989-104">Getting Started with the Data Protection APIs</span></span>

<a name="security-data-protection-getting-started"></a>

<span data-ttu-id="b7989-105">가장 간단 하 고 보호 데이터에는 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-105">At its simplest, protecting data consists of the following steps:</span></span>

1. <span data-ttu-id="b7989-106">데이터 보호 공급자에서 데이터 보호자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-106">Create a data protector from a data protection provider.</span></span>

2. <span data-ttu-id="b7989-107">호출의 `Protect` 메서드 보호 하려는 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-107">Call the `Protect` method with the data you want to protect.</span></span>

3. <span data-ttu-id="b7989-108">호출 된 `Unprotect` 다시 일반 텍스트로 변환 하려는 데이터와 메서드.</span><span class="sxs-lookup"><span data-stu-id="b7989-108">Call the `Unprotect` method with the data you want to turn back into plain text.</span></span>

<span data-ttu-id="b7989-109">대부분의 프레임 워크 및 ASP.NET SignalR, 등의 응용 프로그램 모델 데이터 보호 시스템을 구성 하 고 종속성 주입을 통해 액세스 하는 서비스 컨테이너에 추가 이미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-109">Most frameworks and app models, such as ASP.NET or SignalR, already configure the data protection system and add it to a service container you access via dependency injection.</span></span> <span data-ttu-id="b7989-110">다음 예제에서는 종속성 주입을 위한 서비스 컨테이너를 구성 하 고 등록 하는 데이터 보호 스택의 DI 통해 데이터 보호 공급자를 수신, 보호기 및 보호 한 후 보호 해제 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="b7989-110">The following sample demonstrates configuring a service container for dependency injection and registering the data protection stack, receiving the data protection provider via DI, creating a protector and protecting then unprotecting data</span></span>

[!code-csharp[Main](../../security/data-protection/using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]

<span data-ttu-id="b7989-111">하나 이상을 제공 해야 합니다는 보호기를 만들 때 [목적 문자열](consumer-apis/purpose-strings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-111">When you create a protector you must provide one or more [Purpose Strings](consumer-apis/purpose-strings.md).</span></span> <span data-ttu-id="b7989-112">소비자 간에 격리를 제공 하는 목적은 문자열.</span><span class="sxs-lookup"><span data-stu-id="b7989-112">A purpose string provides isolation between consumers.</span></span> <span data-ttu-id="b7989-113">예를 들어 "녹색"의 목적은 문자열을 사용 하 여 만든 보호기 "자주색"의 용도 보호기에서 제공 되는 데이터를 보호할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-113">For example, a protector created with a purpose string of "green" would not be able to unprotect data provided by a protector with a purpose of "purple".</span></span>

>[!TIP]
> <span data-ttu-id="b7989-114">인스턴스 `IDataProtectionProvider` 및 `IDataProtector` 여러 호출자에 대 한 스레드로부터 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-114">Instances of `IDataProtectionProvider` and `IDataProtector` are thread-safe for multiple callers.</span></span> <span data-ttu-id="b7989-115">구성 요소에 대 한 참조를 가져온 후 사용 하는 `IDataProtector` 호출을 통해 `CreateProtector`, 해당 참조를 여러 번 호출에 사용할 `Protect` 및 `Unprotect`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-115">It is intended that once a component gets a reference to an `IDataProtector` via a call to `CreateProtector`, it will use that reference for multiple calls to `Protect` and `Unprotect`.</span></span>
>
><span data-ttu-id="b7989-116">에 대 한 호출 `Unprotect` CryptographicException 보호 된 페이로드를 확인 하거나 해독할 수 없는 경우이 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-116">A call to `Unprotect` will throw CryptographicException if the protected payload cannot be verified or deciphered.</span></span> <span data-ttu-id="b7989-117">일부 구성 요소 오류를 무시 하려는 경우가 있을 수 하는 동안 작업을 보호 해제 인증 쿠키를 읽는 구성 요소 수 있습니다이 오류를 처리 하 고 전혀 쿠키가 없는 이전의 요청 처럼 처리할 대신 완전 한 요청에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-117">Some components may wish to ignore errors during unprotect operations; a component which reads authentication cookies might handle this error and treat the request as if it had no cookie at all rather than fail the request outright.</span></span> <span data-ttu-id="b7989-118">구체적으로이 동작을 방지 하는 구성 요소는 모든 예외를 받아들이지 않고 CryptographicException을 catch 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7989-118">Components which want this behavior should specifically catch CryptographicException instead of swallowing all exceptions.</span></span>
