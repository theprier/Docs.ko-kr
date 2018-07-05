---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
title: ASP.NET Web API OData 5.3의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: e39eaa25-83ff-41dc-869d-3818d59a88ae
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
msc.type: authoredcontent
ms.openlocfilehash: aedc4e0dc1bf144239f6921a51eaef459a0907a6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386684"
---
<a name="whats-new-in-aspnet-web-api-odata-53"></a><span data-ttu-id="b6468-102">ASP.NET Web API OData 5.3의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b6468-102">What's New in ASP.NET Web API OData 5.3</span></span>
====================
<span data-ttu-id="b6468-103">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b6468-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="b6468-104">이 항목에서는 ASP.NET Web API OData 5.3의 새로운 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-104">This topic describes what's new for ASP.NET Web API OData 5.3.</span></span>

- [<span data-ttu-id="b6468-105">다운로드</span><span class="sxs-lookup"><span data-stu-id="b6468-105">Download</span></span>](#download)
- [<span data-ttu-id="b6468-106">문서</span><span class="sxs-lookup"><span data-stu-id="b6468-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="b6468-107">OData 핵심 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b6468-107">OData Core Libraries</span></span>](#corelib)
- [<span data-ttu-id="b6468-108">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b6468-108">New Features</span></span>](#newf)
- [<span data-ttu-id="b6468-109">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="b6468-109">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="b6468-110">버그 수정</span><span class="sxs-lookup"><span data-stu-id="b6468-110">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="b6468-111">ASP.NET Web API OData 5.3.1의 경우</span><span class="sxs-lookup"><span data-stu-id="b6468-111">ASP.NET Web API OData 5.3.1</span></span>](#OD)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="b6468-112">다운로드</span><span class="sxs-lookup"><span data-stu-id="b6468-112">Download</span></span>

<span data-ttu-id="b6468-113">NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-113">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="b6468-114">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-114">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="b6468-115">설명서</span><span class="sxs-lookup"><span data-stu-id="b6468-115">Documentation</span></span>

<span data-ttu-id="b6468-116">자습서 및 기타 설명서에서 ASP.NET Web API OData에 대 한 있습니다 합니다 [ASP.NET 웹 사이트](../odata-support-in-aspnet-web-api/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-116">You can find tutorials and other documentation about ASP.NET Web API OData at the [ASP.NET web site](../odata-support-in-aspnet-web-api/index.md).</span></span>

<a id="corelib"></a>
## <a name="odata-core-libraries"></a><span data-ttu-id="b6468-117">OData 핵심 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b6468-117">OData Core Libraries</span></span>

<span data-ttu-id="b6468-118">OData v4, Web API 이제 사용 되는 ODataLib 6.5.0 버전</span><span class="sxs-lookup"><span data-stu-id="b6468-118">For OData v4, Web API now uses ODataLib version 6.5.0</span></span>

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-odata-53"></a><span data-ttu-id="b6468-119">ASP.NET의 새로운 기능은 Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="b6468-119">New Features in ASP.NET Web API OData 5.3</span></span>

### <a name="support-for-levels-in-expand"></a><span data-ttu-id="b6468-120">$에서 $Levels에 대 한 지원 확장</span><span class="sxs-lookup"><span data-stu-id="b6468-120">Support for $levels in $expand</span></span>

<span data-ttu-id="b6468-121">$levels를 사용할 수 있습니다 쿼리 옵션에서 $ 쿼리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-121">You can use the $levels query option in $expand queries.</span></span> <span data-ttu-id="b6468-122">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="b6468-122">For example:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample2.cmd)]

<span data-ttu-id="b6468-123">이 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-123">This query is equivalent to:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample3.cmd)]

<a id="open-entity-types"></a>
### <a name="support-for-open-entity-types"></a><span data-ttu-id="b6468-124">개방형 엔터티 형식에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="b6468-124">Support for Open Entity Types</span></span>

<span data-ttu-id="b6468-125">*형식을 열* stuctured 형식이 형식 정의에서 선언 된 속성 외에 동적 속성을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-125">An *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="b6468-126">개방형 형식 데이터 모델에 유연성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-126">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="b6468-127">자세한 내용은 xxxx을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b6468-127">For more information, see xxxx.</span></span>

### <a name="support-for-dynamic-collection-properties-in-open-types"></a><span data-ttu-id="b6468-128">개방형 형식에서 동적 컬렉션 속성에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="b6468-128">Support for dynamic collection properties in open types</span></span>

<span data-ttu-id="b6468-129">이전에 동적 속성을 단일 값 이어야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-129">Previously, a dynamic property had to be a single value.</span></span> <span data-ttu-id="b6468-130">5.3에서 동적 속성 컬렉션 값을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-130">In 5.3, dynamic properties can have collection values.</span></span> <span data-ttu-id="b6468-131">예를 들어 다음 JSON 페이로드를에서 `Emails` 속성 동적 속성 이며 문자열 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-131">For example, in the following JSON payload, the `Emails` property is a dynamic property and is of collection of string type:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample4.cmd)]

### <a name="support-for-inheritance-for-complex-types"></a><span data-ttu-id="b6468-132">복합 형식에 대 한 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="b6468-132">Support for inheritance for complex types</span></span>

<span data-ttu-id="b6468-133">이제 복합 형식의 기본 형식에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-133">Now complex types can inherit from a base type.</span></span> <span data-ttu-id="b6468-134">예를 들어, OData 서비스에는 다음 복합 유형 정의할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="b6468-134">For example, an OData service could define the following complex types:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample5.cs)]

<span data-ttu-id="b6468-135">EDM이 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-135">Here is the EDM for this example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample6.xml?highlight=8,15)]

<span data-ttu-id="b6468-136">자세한 내용은 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-136">For more information, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="b6468-137">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="b6468-137">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="b6468-138">이 섹션에서는 알려진된 문제 및 ASP.NET Web API OData 5.3의 주요 변경 내용에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-138">This section describes known issues and breaking changes in the ASP.NET Web API OData 5.3.</span></span>

### <a name="odata-v4"></a><span data-ttu-id="b6468-139">OData v4</span><span class="sxs-lookup"><span data-stu-id="b6468-139">OData v4</span></span>

#### <a name="query-options"></a><span data-ttu-id="b6468-140">쿼리 옵션</span><span class="sxs-lookup"><span data-stu-id="b6468-140">Query Options</span></span>

<span data-ttu-id="b6468-141">문제: 중첩 된 $를 사용 하 여 $levels를 사용 하 여 확장 = 잘못 된 확장 깊이에서 최대 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-141">Issue: Using nested $expand with $levels=max results in an incorrect expansion depth.</span></span>

<span data-ttu-id="b6468-142">예를 들어 다음 요청:</span><span class="sxs-lookup"><span data-stu-id="b6468-142">For example, given the following request:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample7.cmd)]

<span data-ttu-id="b6468-143">경우 `MaxExpansionDepth` 가 5 이면 6의 확장 깊이이 쿼리를 초래 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-143">If `MaxExpansionDepth` is 5, this query would result in an expansion depth of 6.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="b6468-144">버그 수정 및 사소한 기능 업데이트</span><span class="sxs-lookup"><span data-stu-id="b6468-144">Bug Fixes and Minor Feature Updates</span></span>

<span data-ttu-id="b6468-145">여러 버그 수정 및 사소한 기능에도이 릴리스에서 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-145">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="b6468-146">여기서 전체 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-146">You can find the complete list here:</span></span>

- [<span data-ttu-id="b6468-147">버그 수정</span><span class="sxs-lookup"><span data-stu-id="b6468-147">Bug fixes</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.3%20Beta&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="OD"></a>
## <a name="aspnet-web-api-odata-531"></a><span data-ttu-id="b6468-148">ASP.NET Web API OData 5.3.1의 경우</span><span class="sxs-lookup"><span data-stu-id="b6468-148">ASP.NET Web API OData 5.3.1</span></span>

<span data-ttu-id="b6468-149">이 이번에는 [버그](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.3.1%20Beta&amp;assignedTo=All&amp;component=Web%20API%20OData&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=All) AllowedFunctions 열거형의 일부에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-149">In this release we made a [bug fix](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.3.1%20Beta&amp;assignedTo=All&amp;component=Web%20API%20OData&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=All) to some of the AllowedFunctions enums.</span></span> <span data-ttu-id="b6468-150">이 릴리스에 버그 수정 또는 새로운 기능 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6468-150">This release doesn't have any other bug fixes or new features.</span></span>
