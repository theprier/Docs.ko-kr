---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2 부: 도메인 모델 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: cb98f42df411a7ba12ff4566c30ddfbf253253d4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835501"
---
<a name="part-2-creating-the-domain-models"></a><span data-ttu-id="c1b3a-102">2 부: 도메인 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="c1b3a-102">Part 2: Creating the Domain Models</span></span>
====================
<span data-ttu-id="c1b3a-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c1b3a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c1b3a-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c1b3a-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="c1b3a-105">모델 추가</span><span class="sxs-lookup"><span data-stu-id="c1b3a-105">Add Models</span></span>

<span data-ttu-id="c1b3a-106">방법: Entity Framework는 다음과 같은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="c1b3a-107">데이터베이스 중심: 데이터베이스를 사용 하 여 시작 하 고 Entity Framework 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="c1b3a-108">모델 우선: 시각적 모델을 사용 하 여 시작 하 고 Entity Framework에서는 데이터베이스와 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="c1b3a-109">코드 중심: 코드를 사용 하 여 시작 하 고 Entity Framework 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="c1b3a-110">Poco (plain old CLR object)으로 도메인 개체를 정의 하 여 시작 하죠 코드 우선 방식을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="c1b3a-111">코드 우선 방식을 사용 하 여 도메인 개체 예: 거래 또는 지 속성 데이터베이스 계층을 지원 하기 위해 코드를 추가로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="c1b3a-112">(특히 필요가 없습니다에서 상속 하는 [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) 클래스입니다.) Entity Framework에서 데이터베이스 스키마를 만드는 방법을 제어 하려면 데이터 주석을 여전히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="c1b3a-113">Poco 설명 하는 모든 추가 속성을 전송 하지 않기 때문 [데이터베이스 상태](https://msdn.microsoft.com/library/system.data.entitystate.aspx), JSON 또는 XML로 쉽게 직렬화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="c1b3a-114">그러나 의미는 아닙니다 항상 클라이언트에 직접 Entity Framework 모델을 노출 해야 자습서 뒷부분에서 살펴보겠지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="c1b3a-115">여기서 다음 Poco 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="c1b3a-116">제품</span><span class="sxs-lookup"><span data-stu-id="c1b3a-116">Product</span></span>
- <span data-ttu-id="c1b3a-117">순서</span><span class="sxs-lookup"><span data-stu-id="c1b3a-117">Order</span></span>
- <span data-ttu-id="c1b3a-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="c1b3a-118">OrderDetail</span></span>

<span data-ttu-id="c1b3a-119">각 클래스를 만들려면 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="c1b3a-120">상황에 맞는 메뉴에서 선택 **추가** 를 선택한 **클래스입니다.**</span><span class="sxs-lookup"><span data-stu-id="c1b3a-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="c1b3a-121">추가 된 `Product` 다음 구현 클래스:</span><span class="sxs-lookup"><span data-stu-id="c1b3a-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="c1b3a-122">Entity Framework 사용 규칙에 따라는 `Id` 속성을 기본 키로 데이터베이스 테이블에 id 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="c1b3a-123">새로 만들 때 `Product` 경우에 대 한 값을 설정 하지 `Id`이므로 데이터베이스에서 값을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="c1b3a-124">합니다 **ScaffoldColumn** 특성은 표시 하지 않으려면 ASP.NET MVC를 지시를 `Id` 편집기 폼을 생성할 때 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="c1b3a-125">합니다 **필요한** 특성 모델의 유효성을 검사 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="c1b3a-126">지정 된 `Name` 속성은 비어 있지 않은 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="c1b3a-127">추가 된 `Order` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c1b3a-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="c1b3a-128">추가 된 `OrderDetail` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c1b3a-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="c1b3a-129">외래 키 관계</span><span class="sxs-lookup"><span data-stu-id="c1b3a-129">Foreign Key Relations</span></span>

<span data-ttu-id="c1b3a-130">주문을 여러 주문 세부 정보를 포함 하 고 각 주문 세부 정보를 단일 제품을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="c1b3a-131">이러한 관계를 나타내는 합니다 `OrderDetail` 라는 속성을 정의 하는 클래스 `OrderId` 및 `ProductId`합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="c1b3a-132">Entity Framework는 이러한 속성 외래 키를 나타내고 데이터베이스에 외래 키 제약 조건 추가 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="c1b3a-133">합니다 `Order` 고 `OrderDetail` 클래스 관련된 개체에 대 한 참조를 포함 하는 "탐색" 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="c1b3a-134">순서 지정, 탐색 속성에 따라 순서 대로 제품을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="c1b3a-135">이제 프로젝트를 컴파일하십시오.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-135">Compile the project now.</span></span> <span data-ttu-id="c1b3a-136">Entity Framework 리플렉션을 사용 하 여 컴파일된 어셈블리를 데이터베이스 스키마를 만들어야 하므로 모델의 속성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="c1b3a-137">미디어 유형 포맷터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="c1b3a-138">A [미디어 유형 포맷터](../../formats-and-model-binding/media-formatters.md) 는 Web API HTTP 응답 본문을 쓸 때 데이터를 serialize 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="c1b3a-139">기본 제공 포맷터 JSON 및 XML 출력을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="c1b3a-140">기본적으로 값으로 모든 개체를 serialize 모두 이러한 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="c1b3a-141">Serialization 값으로 개체 그래프에 순환 참조가 포함 된 경우 문제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="c1b3a-142">이 정확 하 게 사용 하 여 합니다 `Order` 및 `OrderDetail` 다른에 대 한 참조를 유지 하는 각 없으므로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="c1b3a-143">포맷터는 각 개체를 값으로 작성 된 참조에 따라를 제자리에 맴에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="c1b3a-144">따라서 기본 동작을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="c1b3a-145">솔루션 탐색기에서 앱 확장\_폴더를 시작 하 고 WebApiConfig.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="c1b3a-146">`WebApiConfig` 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="c1b3a-147">이 코드는 개체 참조를 유지 하는 JSON 포맷터를 설정 하 고 파이프라인에서 XML 포맷터를 완전히 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="c1b3a-148">(개체 참조를 유지 하는 XML 포맷터를 구성할 수 있습니다 하지만 것이 좀 더 많은 작업 및이 응용 프로그램에 대 한 JSON만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1b3a-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="c1b3a-149">자세한 내용은 [개체 순환 참조가 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span><span class="sxs-lookup"><span data-stu-id="c1b3a-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1b3a-150">[이전](using-web-api-with-entity-framework-part-1.md)
> [다음](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="c1b3a-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
