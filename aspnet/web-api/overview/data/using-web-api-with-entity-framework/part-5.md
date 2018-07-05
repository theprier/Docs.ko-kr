---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 (Dto) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: a1be1b72559aaffdf530402313f58d6c2e25b189
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828165"
---
<a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="f81eb-102">데이터 전송 개체 (Dto) 만들기</span><span class="sxs-lookup"><span data-stu-id="f81eb-102">Create Data Transfer Objects (DTOs)</span></span>
====================
<span data-ttu-id="f81eb-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f81eb-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f81eb-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f81eb-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="f81eb-105">이제 오른쪽 웹 API 클라이언트에 데이터베이스 엔터티를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="f81eb-106">클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="f81eb-107">그러나 없는 항상 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-107">However, that's not always a good idea.</span></span> <span data-ttu-id="f81eb-108">클라이언트에 보내는 데이터의 모양을 변경 하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="f81eb-109">예를 들어, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-109">For example, you might want to:</span></span>

- <span data-ttu-id="f81eb-110">(이전 섹션 참조) 하는 순환 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="f81eb-111">클라이언트를 보려면 해야 하지는 특정 속성을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="f81eb-112">페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="f81eb-113">클라이언트에 대 한 편리한 있도록 중첩 된 개체를 포함 하는 개체 그래프를 평면화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="f81eb-114">"과도 한 게시" 취약점을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="f81eb-115">(참조 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 과도 한 게시에 대 한 내용은.)</span><span class="sxs-lookup"><span data-stu-id="f81eb-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="f81eb-116">데이터베이스 계층에서 서비스 계층을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="f81eb-117">이를 위해 정의할 수 있습니다는 *데이터 전송 개체* (DTO).</span><span class="sxs-lookup"><span data-stu-id="f81eb-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="f81eb-118">DTO는 네트워크를 통해 데이터가 전송 되는 방법을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="f81eb-119">책 엔터티와 작동 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="f81eb-120">Models 폴더에서 두 개의 DTO 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="f81eb-121">합니다 `BookDetailDTO` 클래스를 포함 한다는 점을 제외 하는 책 모델에서 속성을 모두 `AuthorName` 작성자 이름을 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="f81eb-122">합니다 `BookDTO` 클래스에서 속성의 하위 집합을 포함 `BookDetailDTO`합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="f81eb-123">두 개의 GET 메서드를 다음으로 대체 합니다 `BooksController` Dto를 반환 하는 버전을 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="f81eb-124">LINQ를 사용 하 여 **선택** 책 엔터티에서 Dto로 변환 하는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="f81eb-125">다음은 새 생성 된 SQL `GetBooks` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f81eb-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="f81eb-126">EF에 LINQ 변환는 볼 수 있습니다 **선택** SQL SELECT 문으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="f81eb-127">마지막으로 수정 된 `PostBook` DTO를 반환 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="f81eb-128">이 자습서에서는 것으로 변환 하 고 Dto로 수동으로 코드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="f81eb-129">같은 라이브러리를 사용 하는 다른 옵션도 [AutoMapper](http://automapper.org/) 변환이 자동으로 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81eb-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="f81eb-130">[이전](part-4.md)
> [다음](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="f81eb-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
