---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API 사용 하 여 OData v4의 복합 형식 상속은 | Microsoft Docs
author: microsoft
description: OData v4 사양에 따라 복합 형식은 다른 복합 형식에서 상속할 수 있습니다. (복합 형식은 키가 없는 구조적된 형식을.) Web API는 중...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 8dbf7dc4cfc70e1ea1ed6f72ffc0751a56809c09
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839095"
---
<a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="82b09-104">ASP.NET Web API 사용 하 여 OData v4의 복합 형식 상속</span><span class="sxs-lookup"><span data-stu-id="82b09-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="82b09-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="82b09-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="82b09-106">OData v4에 따라 [사양](http://www.odata.org/documentation/odata-version-4-0/), 복합 형식은 다른 복합 형식에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="82b09-107">(A *복잡 한* 형식은 키가 없는 구조적된 형식입니다.) Web API OData 5.3 복합 형식 상속은 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="82b09-108">이 항목에서는 복잡 한 상속 형식을 사용 하 여 엔터티 데이터 모델 (EDM)를 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="82b09-109">전체 소스 코드를 보려면 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="82b09-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="82b09-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="82b09-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="82b09-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="82b09-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="82b09-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="82b09-113">모델 계층 구조</span><span class="sxs-lookup"><span data-stu-id="82b09-113">Model Hierarchy</span></span>

<span data-ttu-id="82b09-114">복합 형식 상속은 보여 주기 위해 다음 클래스 계층 구조를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="82b09-115">`Shape` 추상 복합 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="82b09-116">`Rectangle`를 `Triangle`, 및 `Circle` 에서 파생 된 복합 형식 `Shape`, 및 `RoundRectangle` 에서 파생 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="82b09-117">`Window` 엔터티 형식 및 포함 된 `Shape` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="82b09-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="82b09-118">이러한 형식을 정의 하는 CLR 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="82b09-119">EDM 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="82b09-119">Build the EDM Model</span></span>

<span data-ttu-id="82b09-120">EDM을 만들려면 사용할 수 있습니다 **ODataConventionModelBuilder**, CLR 형식에서 상속 관계를 유추 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="82b09-121">빌드할 수도 있습니다 EDM 명시적으로 사용 하 여 **된 ODataModelBuilder**합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="82b09-122">더 많은 코드를 걸리지만 EDM 통해 더 많은 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="82b09-123">이러한 두 예제에서는 동일한 EDM 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="82b09-124">메타 데이터 문서</span><span class="sxs-lookup"><span data-stu-id="82b09-124">Metadata Document</span></span>

<span data-ttu-id="82b09-125">복합 형식 상속을 보여 주는 OData 메타 데이터 문서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="82b09-126">메타 데이터 문서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="82b09-127">`Shape` 복합 형식이 추상 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="82b09-128">합니다 `Rectangle`, `Triangle`, 및 `Circle` 복합 형식의 기본 형식이 `Shape`합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="82b09-129">합니다 `RoundRectangle` 형식은 기본 형식 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="82b09-130">복합 형식 캐스팅</span><span class="sxs-lookup"><span data-stu-id="82b09-130">Casting Complex Types</span></span>

<span data-ttu-id="82b09-131">복합 형식에서 캐스팅 이제 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="82b09-132">예를 들어 다음 쿼리 캐스트를 `Shape` 에 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="82b09-133">응답 페이로드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82b09-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
