---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 Dto ()를 만들 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 35e01f959072b96204de3e2ce3d507635720e110
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878687"
---
<a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="4f0c9-102">데이터 전송 개체 (Dto) 만들기</span><span class="sxs-lookup"><span data-stu-id="4f0c9-102">Create Data Transfer Objects (DTOs)</span></span>
====================
<span data-ttu-id="4f0c9-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4f0c9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4f0c9-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4f0c9-105">이제, 오른쪽 웹 API를 클라이언트 데이터베이스 엔터티를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="4f0c9-106">클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="4f0c9-107">그러나 없는 항상는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-107">However, that's not always a good idea.</span></span> <span data-ttu-id="4f0c9-108">클라이언트에 보낸 데이터의 모양을 변경 하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="4f0c9-109">예를 들어, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-109">For example, you might want to:</span></span>

- <span data-ttu-id="4f0c9-110">(이전 단원 참조) 순환 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="4f0c9-111">클라이언트를 보려면 안 특정 속성을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="4f0c9-112">페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="4f0c9-113">클라이언트에 대 한 더 편리 하 게 하려면 중첩 된 개체를 포함 하는 개체 그래프를 평면화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="4f0c9-114">"게시 과도 하 게" 보안 문제를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="4f0c9-115">(참조 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 과도 하 게 게시에 대 한 내용은.)</span><span class="sxs-lookup"><span data-stu-id="4f0c9-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="4f0c9-116">데이터베이스 계층에서 서비스 계층을 통해 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="4f0c9-117">이를 위해 정의할 수 있습니다는 *데이터 전송 개체* (DTO).</span><span class="sxs-lookup"><span data-stu-id="4f0c9-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="4f0c9-118">한 DTO는 네트워크를 통해 데이터가 전송 되는 방법을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="4f0c9-119">책 엔터티와 함께 작동 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="4f0c9-120">모델 폴더에서 두 개의 DTO 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="4f0c9-121">`BookDetailDTO` 클래스는 점을 제외 하 고 책 모델에서 속성을 모두 포함 `AuthorName` 사람의 이름을 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="4f0c9-122">`BookDTO` 클래스에서 속성의 하위 집합에 포함 되어 `BookDetailDTO`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="4f0c9-123">두 개의 GET 메서드를 다음으로 바꾸기는 `BooksController` Dto 반환 하는 버전의 클래스.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="4f0c9-124">LINQ를 사용 합니다 **선택** 책 엔터티에서 Dto로 변환 하는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="4f0c9-125">다음은 새에 의해 생성 된 SQL `GetBooks` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="4f0c9-126">EF LINQ 변환 있는지 확인할 수 있습니다 **선택** SQL SELECT 문으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="4f0c9-127">마지막으로 수정 된 `PostBook` 메서드를 한 DTO 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="4f0c9-128">이 자습서에서는 변환 대상 Dto 수동으로 코드에서.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="4f0c9-129">또 다른 옵션은 같은 라이브러리를 사용 하도록 [AutoMapper](http://automapper.org/) 변환이 자동으로 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0c9-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="4f0c9-130">[이전](part-4.md)
> [다음](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="4f0c9-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
