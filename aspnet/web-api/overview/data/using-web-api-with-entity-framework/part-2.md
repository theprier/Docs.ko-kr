---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: "모델 및 컨트롤러를 추가 합니다. | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 7e09316f0faaf0731e4cdda48040fdaedc0f244a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="add-models-and-controllers"></a><span data-ttu-id="6286d-102">모델 및 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-102">Add Models and Controllers</span></span>
====================
<span data-ttu-id="6286d-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6286d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6286d-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="6286d-105">이 섹션에서는 데이터베이스 엔터티를 정의 하는 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="6286d-106">그런 다음 이러한 엔터티에 대 한 CRUD 작업을 수행 하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="6286d-107">모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-107">Add Model Classes</span></span>

<span data-ttu-id="6286d-108">이 자습서에서는 "Code First" 접근 방식 Entity Framework (EF)를 사용 하 여 데이터베이스를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="6286d-109">Code First를 데이터베이스 테이블에 해당 하는 C# 클래스를 작성 하 고 EF 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="6286d-110">(자세한 내용은 참조 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="6286d-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="6286d-111">도메인 개체 POCOs (일반 이전 CLR 개체)으로 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="6286d-112">다음 POCOs을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="6286d-113">만든 이</span><span class="sxs-lookup"><span data-stu-id="6286d-113">Author</span></span>
- <span data-ttu-id="6286d-114">북</span><span class="sxs-lookup"><span data-stu-id="6286d-114">Book</span></span>

<span data-ttu-id="6286d-115">솔루션 탐색기에서 마우스 오른쪽 단추로 모델 폴더를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="6286d-116">선택 **추가**을 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="6286d-117">클래스 이름을 `Author`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="6286d-118">모든 Author.cs에 상용구 코드 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="6286d-119">라는 다른 클래스를 추가 `Book`, 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="6286d-120">Entity Framework 데이터베이스 테이블을 만드는 이러한 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="6286d-121">각 모델에 대해는 `Id` 속성은 데이터베이스 테이블의 기본 키 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="6286d-122">Book 클래스에는 `AuthorId` 에 외래 키 정의 `Author` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="6286d-123">(간단한 설명을 위해 필자가 가정 하 고 각 책에는 단일 작성자입니다.) 책 클래스는 관련 항목에 탐색 속성이 포함 되어 `Author`합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="6286d-124">탐색 속성을 사용 하 여 관련 액세스 `Author` 코드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="6286d-125">내가 말하는 바로 그 4, 부분에 탐색 속성에 대 한 자세한 [처리 엔터티 관계](part-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="6286d-126">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="6286d-126">Add Web API Controllers</span></span>

<span data-ttu-id="6286d-127">이 섹션에서는 Web API 컨트롤러 CRUD 작업을 지 원하는 추가 합니다 (만들기, 읽기, 업데이트 및 삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="6286d-128">데이터베이스 계층와 통신 하는 컨트롤러 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="6286d-129">첫째, Controllers/ValuesController.cs 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="6286d-130">이 파일에는 예제 웹 API 컨트롤러 포함 되어 있지만이 자습서에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="6286d-131">다음으로 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="6286d-131">Next, build the project.</span></span> <span data-ttu-id="6286d-132">Web API 스 캐 폴딩 리플렉션을 사용 하 여 되므로 컴파일된 어셈블리 원래 모델 클래스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="6286d-133">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6286d-134">선택 **추가**을 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="6286d-135">에 **추가 스 캐 폴드** 대화 상자에서 "Web API 2 Entity Framework를 사용 하 여 작업, 컨트롤러"입니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="6286d-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="6286d-137">에 **컨트롤러 추가** 대화 상자에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="6286d-138">에 **모델 클래스** 드롭다운을 선택 된 `Author` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="6286d-139">(경우 보이지 않으면 드롭다운에 나열 된 것을 해야 프로젝트를 빌드.)</span><span class="sxs-lookup"><span data-stu-id="6286d-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="6286d-140">"비동기 컨트롤러 동작 사용"을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="6286d-141">으로 컨트롤러 이름을 둡니다 &quot;AuthorsController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="6286d-142">클릭 더하기 (+) 단추 옆에 **데이터 컨텍스트 클래스가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="6286d-143">에 **새 데이터 컨텍스트에** 대화 상자에서 기본 이름을 그대로 두고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="6286d-144">클릭 **추가** 완료 하는 **컨트롤러 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6286d-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="6286d-145">프로젝트에 두 개의 클래스를 추가 하는 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="6286d-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="6286d-146">`AuthorsController`Web API 컨트롤러를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="6286d-147">컨트롤러는 클라이언트가 사용 작성자의 목록에서 CRUD 작업을 수행 하는 REST API를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="6286d-148">`BookServiceContext`데이터베이스에 데이터는 데이터베이스, 변경 내용 추적 및 데이터 유지를 사용 하 여 개체를 채우는 포함 하는 런타임 시 엔터티 개체를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="6286d-149">상속 된 `DbContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="6286d-150">이 시점에서 프로젝트를 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="6286d-150">At this point, build the project again.</span></span> <span data-ttu-id="6286d-151">에 대 한 API 컨트롤러를 추가 하려면 동일한 단계를 수행해 이제 `Book` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6286d-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="6286d-152">선택이 시간 `Book` 기존 선택한 모델 클래스에 대 한 `BookServiceContext` 데이터 컨텍스트 클래스에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="6286d-153">(새 데이터 컨텍스트를 만들지 않습니다.) 클릭 **추가** 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6286d-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

>[!div class="step-by-step"]
<span data-ttu-id="6286d-154">[이전](part-1.md)
[다음](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="6286d-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
