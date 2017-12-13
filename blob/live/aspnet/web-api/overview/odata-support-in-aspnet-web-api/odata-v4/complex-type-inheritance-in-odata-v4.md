---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: "ASP.NET web API OData v4에 복합 유형 상속이 | Microsoft Docs"
author: microsoft
description: "OData v4 사양에 복합 유형을 다른 복합 형식에서 상속할 수 있습니다. (복합 형식은 키가 없는 구조적된 형식이입니다.) Web API 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: be2dbfa82b99b6c48928e4e767716852c14a463b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="ad4b0-104">ASP.NET Web API 사용 하 여 OData v4에 복합 형식 상속</span><span class="sxs-lookup"><span data-stu-id="ad4b0-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="ad4b0-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ad4b0-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ad4b0-106">OData v 4에 따라 [사양](http://www.odata.org/documentation/odata-version-4-0/), 복합 형식 다른 복합 형식에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="ad4b0-107">(A *복잡 한* 형식은 키가 없는 구조적된 형식입니다.) Web API OData 5.3 복합 유형 상속이 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="ad4b0-108">이 항목에서는 복잡 한 상속 형식 (EDM)는 엔터티 데이터 모델을 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="ad4b0-109">전체 소스 코드에 대 한 참조 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ad4b0-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ad4b0-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ad4b0-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="ad4b0-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="ad4b0-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="ad4b0-112">OData v4</span></span>


## <a name="model-hierarchy"></a><span data-ttu-id="ad4b0-113">모델 계층 구조</span><span class="sxs-lookup"><span data-stu-id="ad4b0-113">Model Hierarchy</span></span>

<span data-ttu-id="ad4b0-114">복합 유형 상속이 보여 주기 위해 다음과 같은 클래스 계층 구조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="ad4b0-115">`Shape`추상 복합 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="ad4b0-116">`Rectangle``Triangle`, 및 `Circle` 에서 파생 된 복합 형식을 `Shape`, 및 `RoundRectangle` 에서 파생 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="ad4b0-117">`Window`엔터티 형식 및 포함 된 `Shape` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="ad4b0-118">다음은 이러한 형식을 정의 하는 CLR 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="ad4b0-119">EDM 모델을 작성</span><span class="sxs-lookup"><span data-stu-id="ad4b0-119">Build the EDM Model</span></span>

<span data-ttu-id="ad4b0-120">EDM을 만들려면 사용할 수 있습니다 **ODataConventionModelBuilder**, CLR 형식에서 상속 관계를 유추 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="ad4b0-121">빌드할 수도 있습니다는 EDM 명시적으로 사용 하 여 **된**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="ad4b0-122">더 많은 코드 걸리지만 EDM 보다 상세하게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="ad4b0-123">이러한 두 가지 예는 동일한 EDM 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="ad4b0-124">메타 데이터 문서</span><span class="sxs-lookup"><span data-stu-id="ad4b0-124">Metadata Document</span></span>

<span data-ttu-id="ad4b0-125">복합 형식 상속을 보여 주는 OData 메타 데이터 문서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="ad4b0-126">메타 데이터 문서에서을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="ad4b0-127">`Shape` 복합 형식이 추상 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="ad4b0-128">`Rectangle`, `Triangle`, 및 `Circle` 복합 유형에 기본 형식을 가질 `Shape`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="ad4b0-129">`RoundRectangle` 형식에 기본 형식이 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="ad4b0-130">복합 형식 캐스팅</span><span class="sxs-lookup"><span data-stu-id="ad4b0-130">Casting Complex Types</span></span>

<span data-ttu-id="ad4b0-131">복합 형식 캐스팅 이제 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="ad4b0-132">예를 들어 다음 쿼리 캐스트는 `Shape` 에 `Rectangle`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="ad4b0-133">다음은 응답 페이로드가입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4b0-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
