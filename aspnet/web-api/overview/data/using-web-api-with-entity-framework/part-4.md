---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 엔터티 관계를 처리 합니다. | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: 3c82724739b8ccb7c6b13788a5420af1e61c990b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872691"
---
<a name="handling-entity-relations"></a><span data-ttu-id="1ff8c-102">처리 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="1ff8c-102">Handling Entity Relations</span></span>
====================
<span data-ttu-id="1ff8c-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1ff8c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1ff8c-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="1ff8c-105">이 섹션에서는 EF에서 관련된 엔터티를 로드 하는 방법 및 모델 클래스에서 순환 탐색 속성을 처리 하는 방법에 대 한 세부 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="1ff8c-106">(이 섹션 배경 지식을 제공 하 고이 자습서를 완료 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="1ff8c-107">원하는 경우 건너뜁니다 [5 부.](part-5.md).)</span><span class="sxs-lookup"><span data-stu-id="1ff8c-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="1ff8c-108">Eager 지연 로드 및 로드</span><span class="sxs-lookup"><span data-stu-id="1ff8c-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="1ff8c-109">EF는 관계형 데이터베이스를 사용할 경우에 EF 관련된 데이터를 로드 하는 방식을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="1ff8c-110">또한 EF 생성 하는 SQL 쿼리를 확인 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="1ff8c-111">SQL를 추적 하려면 코드의 다음 줄을 추가 `BookServiceContext` 생성자:</span><span class="sxs-lookup"><span data-stu-id="1ff8c-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="1ff8c-112">/Api/books에 GET 요청을 보낼 경우 다음과 같은 JSON 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="1ff8c-113">Author 속성은 null, 책 유효한 AuthorId를 포함 하는 경우에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="1ff8c-114">EF 관련된 만든 엔터티를 로드 하지 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="1ff8c-115">SQL 쿼리 추적 로그에는이 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="1ff8c-116">SELECT 문은 Books 테이블에서 가져오고 만든 테이블을 참조 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="1ff8c-117">참조를 위해 여기의 메서드가 있으며이 `BooksController` 책의 목록을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="1ff8c-118">작성자는 JSON 데이터의 일부로 반환 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="1ff8c-119">Entity Framework의 관련된 데이터를 로드 하는 방법은 세 가지가: 즉시 로드, 지연 로드 및 명시적 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="1ff8c-120">작동 방식을 이해 하는 것이 중요 되기 때문에 각 기술 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="1ff8c-121">즉시 로드</span><span class="sxs-lookup"><span data-stu-id="1ff8c-121">Eager Loading</span></span>

<span data-ttu-id="1ff8c-122">와 *즉시 로드*, EF 초기 데이터베이스 쿼리의 일환으로 관련된 엔터티를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="1ff8c-123">즉시 로드를 수행 하려면는 **System.Data.Entity.Include** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="1ff8c-124">쿼리에서 만든 데이터를 포함 하는 EF를 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="1ff8c-125">이와 같이 변경 하 고 앱을 실행 하는 경우 이제 JSON 데이터 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="1ff8c-126">추적 로그 EF 책 및 만든 테이블에 대해 조인을 수행 함을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="1ff8c-127">지연 로드</span><span class="sxs-lookup"><span data-stu-id="1ff8c-127">Lazy Loading</span></span>

<span data-ttu-id="1ff8c-128">지연 로드 하 여 EF 때 자동으로 로드 관련된 엔터티는 해당 엔터티에 대 한 탐색 속성을 역참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="1ff8c-129">지연 로드를 사용 하도록 설정 하려면 탐색 속성 가상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="1ff8c-130">예를 들어 Book 클래스:</span><span class="sxs-lookup"><span data-stu-id="1ff8c-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="1ff8c-131">이제 다음 코드를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="1ff8c-132">지연 로드를 사용 하는 액세스 하는 `Author` 속성을 `books[0]` 하면 EF 작성자에 대 한 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="1ff8c-133">지연 로드 EF 관련된 엔터티의 검색 될 때마다 쿼리를 전송 하기 때문에 여러 데이터베이스 왕복 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="1ff8c-134">일반적으로 원하는 지연 로딩을 serialize 할 개체에 대 한 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="1ff8c-135">Serializer에 모든 관련된 엔터티 로드를 트리거하는 모델에 속성을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="1ff8c-136">예를 들어 다음은 SQL 쿼리 EF를 사용 하도록 설정 하는 지연 로드 하 여 책 목록을 serialize 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="1ff8c-137">EF는 세 명의 저자에 대 한 세 가지 별도 쿼리를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="1ff8c-138">시간 지연 로드를 사용 하려는 경우 아직 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="1ff8c-139">즉시 로드 매우 복잡 한 조인을 생성 하는 EF를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="1ff8c-140">또는 데이터의 작은 하위 집합에 대 한 관련된 엔터티를 할 수 있습니다 및 지연 로딩 충분히 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="1ff8c-141">Serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="1ff8c-142">문서의 뒷부분에서이 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="1ff8c-143">명시적 로드</span><span class="sxs-lookup"><span data-stu-id="1ff8c-143">Explicit Loading</span></span>

<span data-ttu-id="1ff8c-144">명시적 로드는 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 가져오기 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="1ff8c-145">명시적 로드 관련된 데이터를 로드 하는 경우 보다 자세히 제어를 제공 하지만 추가 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="1ff8c-146">명시적 로드에 대 한 자세한 내용은 참조 [관련 엔터티 로드](https://msdn.microsoft.com/data/jj574232#explicit)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="1ff8c-147">탐색 속성 및 순환 참조</span><span class="sxs-lookup"><span data-stu-id="1ff8c-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="1ff8c-148">탐색 속성에 정의 때 책 목록과 만든 모델을 정의 했습니다는 `Book` 책 만든 관계에 대 한 클래스는 다른 곳에는 탐색 속성 정의 하지 않았으므로 I 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="1ff8c-149">해당 탐색 속성을 추가 하면 어떤 일이 생기는 `Author` 클래스?</span><span class="sxs-lookup"><span data-stu-id="1ff8c-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="1ff8c-150">안타깝게도,이 모델을 serialize 할 때 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="1ff8c-151">관련된 데이터를 로드 하는 경우 순환 개체 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="1ff8c-152">JSON 또는 XML 포맷터를 그래프를 serialize 하려고 하면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="1ff8c-153">두 가지 포맷터는 다른 예외 메시지를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="1ff8c-154">JSON 포맷터에 대 한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="1ff8c-155">XML 포맷터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="1ff8c-156">한 가지 해결 하려면 다음 섹션에서 설명 하는 Dto를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="1ff8c-157">또는 그래프 주기를 처리 하는 JSON과 XML 포맷터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="1ff8c-158">자세한 내용은 참조 [순환 개체 참조를 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="1ff8c-159">이 자습서에서는 필요 하지 않습니다는 `Author.Book` 탐색 속성 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff8c-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ff8c-160">[이전](part-3.md)
> [다음](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="1ff8c-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
