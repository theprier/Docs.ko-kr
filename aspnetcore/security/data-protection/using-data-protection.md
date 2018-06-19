---
title: ASP.NET Core의 데이터 보호 Api 시작
author: rick-anderson
description: 보호 하 고, 응용 프로그램의 데이터를 보호 해제에 대 한 ASP.NET Core 데이터 보호 Api를 사용 하는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/using-data-protection
ms.openlocfilehash: 3a69abd2b58e02f87ccaf2317b0a8a2a7e9d7b4a
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30076990"
---
# <a name="get-started-with-the-data-protection-apis-in-aspnet-core"></a><span data-ttu-id="8d3a8-103">ASP.NET Core의 데이터 보호 Api 시작</span><span class="sxs-lookup"><span data-stu-id="8d3a8-103">Get started with the Data Protection APIs in ASP.NET Core</span></span>

<a name="security-data-protection-getting-started"></a>

<span data-ttu-id="8d3a8-104">데이터 보호 작업을 간단히 정리하면 다음 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-104">At its simplest, protecting data consists of the following steps:</span></span>

1. <span data-ttu-id="8d3a8-105">데이터 보호 공급자를 이용해서 데이터 보호자를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-105">Create a data protector from a data protection provider.</span></span>

2. <span data-ttu-id="8d3a8-106">보호할 데이터를 대상으로 `Protect` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-106">Call the `Protect` method with the data you want to protect.</span></span>

3. <span data-ttu-id="8d3a8-107">평문으로 되돌릴 데이터를 대상으로 `Unprotect` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-107">Call the `Unprotect` method with the data you want to turn back into plain text.</span></span>

<span data-ttu-id="8d3a8-108">ASP.NET이나 SignalR 같은 대부분의 프레임워크 및 앱 모델은 이미 내부적으로 데이터 보호 시스템을 구성해서 서비스 컨테이너에 추가해주기 때문에 종속성 주입을 통해서 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-108">Most frameworks and app models, such as ASP.NET or SignalR, already configure the data protection system and add it to a service container you access via dependency injection.</span></span> <span data-ttu-id="8d3a8-109">다음 예제는 종속성 주입을 위한 서비스 컨테이너의 구성 방법과 데이터 보호 스택을 등록하는 방법, DI를 통해서 데이터 보호 공급자를 가져오는 방법, 보호자를 생성하는 방법, 그리고 데이터를 보호했다가 다시 보호 해제하는 방법을 보여줍니다</span><span class="sxs-lookup"><span data-stu-id="8d3a8-109">The following sample demonstrates configuring a service container for dependency injection and registering the data protection stack, receiving the data protection provider via DI, creating a protector and protecting then unprotecting data</span></span>

[!code-csharp[](../../security/data-protection/using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]

<span data-ttu-id="8d3a8-110">보호자를 생성할 때 반드시 한 개 이상의 [용도 문자열](xref:security/data-protection/consumer-apis/purpose-strings) 을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-110">When you create a protector you must provide one or more [Purpose Strings](xref:security/data-protection/consumer-apis/purpose-strings).</span></span> <span data-ttu-id="8d3a8-111">용도 문자열은 소비자 간의 격리를 제공해주는 역할을 하는데.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-111">A purpose string provides isolation between consumers.</span></span> <span data-ttu-id="8d3a8-112">가령 "green"이라는 용도 문자열을 이용해서 생성된 보호자는 "purple"이라는 용도 문자열을 이용해서 생성된 보호자에 의해 만들어진 데이터의 보호를 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-112">For example, a protector created with a purpose string of "green" wouldn't be able to unprotect data provided by a protector with a purpose of "purple".</span></span>

>[!TIP]
> <span data-ttu-id="8d3a8-113">`IDataProtectionProvider` 및 `IDataProtector` 의 인스턴스는 다중 호출자에 대해 스레드로부터 안전(Thread-Safe)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-113">Instances of `IDataProtectionProvider` and `IDataProtector` are thread-safe for multiple callers.</span></span> <span data-ttu-id="8d3a8-114">구성 요소에서 `CreateProtector` 를 호출해서 `IDataProtector` 의 참조를 얻은 다음, 이 참조를 이용해서 `Protect` 및 `Unprotect` 를 반복적으로 호출할 수 있도록 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-114">It's intended that once a component gets a reference to an `IDataProtector` via a call to `CreateProtector`, it will use that reference for multiple calls to `Protect` and `Unprotect`.</span></span>
>
><span data-ttu-id="8d3a8-115">`Unprotect` 호출 시 보호된 페이로드를 검증하거나 판독할 수 없으면 `CryptographicException`이 던져집니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-115">A call to `Unprotect` will throw CryptographicException if the protected payload cannot be verified or deciphered.</span></span> <span data-ttu-id="8d3a8-116">일부 구성 요소는 보호 해제 작업 중 발생하는 오류를 무시해야 하는 경우도 있는데, 가령 인증 쿠키를 읽는 구성 요소는 요청 자체를 실패시키는 대신 이 오류를 처리하여 쿠키가 아예 존재하지 않는 것처럼 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-116">Some components may wish to ignore errors during unprotect operations; a component which reads authentication cookies might handle this error and treat the request as if it had no cookie at all rather than fail the request outright.</span></span> <span data-ttu-id="8d3a8-117">이런 동작이 필요한 구성 요소는 모든 예외를 감춰버리는 대신 명확하게 `CryptographicException`만 잡아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3a8-117">Components which want this behavior should specifically catch CryptographicException instead of swallowing all exceptions.</span></span>
