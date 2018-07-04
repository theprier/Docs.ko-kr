---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3 부: 관리 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: b9d21edec7b5006beea83395cdfc5ae181992e7d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365047"
---
<a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="dae4e-102">3 부: 관리 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="dae4e-102">Part 3: Creating an Admin Controller</span></span>
====================
<span data-ttu-id="dae4e-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dae4e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="dae4e-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="dae4e-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="dae4e-105">관리 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-105">Add an Admin Controller</span></span>

<span data-ttu-id="dae4e-106">이 섹션에서는 CRUD를 지 원하는 웹 API 컨트롤러를 추가 합니다 (만들기, 읽기, 업데이트 및 삭제) 제품에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="dae4e-107">컨트롤러는 데이터베이스 계층을 사용 하 여 통신 하도록 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="dae4e-108">관리자만이 컨트롤러를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="dae4e-109">고객은 다른 컨트롤러를 통해 제품을 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="dae4e-110">솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="dae4e-111">선택 **추가할** 차례로 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="dae4e-112">에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 `AdminController`입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="dae4e-113">아래 **템플릿을**를 선택 &quot;읽기/쓰기 작업을 Entity Framework를 사용 하 여 포함 된 API 컨트롤러&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="dae4e-114">아래 **모델 클래스**, "Product (ProductStore.Models)"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="dae4e-115">아래 **데이터 컨텍스트**을 선택 "&lt;새 데이터 컨텍스트에&gt;"입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="dae4e-116">경우는 **모델 클래스** 드롭다운 표시 하지 않습니다 모든 모델 클래스를 프로젝트를 컴파일 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="dae4e-117">Entity Framework 컴파일된 어셈블리를 해야 하므로 리플렉션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>


<span data-ttu-id="dae4e-118">선택 "&lt;새 데이터 컨텍스트에&gt;" 열립니다 합니다 **새 데이터 컨텍스트에** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="dae4e-119">데이터 컨텍스트 이름을 `ProductStore.Models.OrdersContext`입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="dae4e-120">클릭 **확인** 해제 하는 **새 데이터 컨텍스트에** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="dae4e-121">에 **컨트롤러 추가** 대화 상자에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="dae4e-122">프로젝트에 추가 되었습니다 기능 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="dae4e-123">클래스가 `OrdersContext` 에서 파생 된 **DbContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="dae4e-124">이 클래스는 POCO 모델 및 데이터베이스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="dae4e-125">명명 된 Web API 컨트롤러 `AdminController`합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="dae4e-126">이 컨트롤러에서 CRUD 작업 지원 `Product` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="dae4e-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="dae4e-127">사용 된 `OrdersContext` Entity Framework와 통신 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="dae4e-128">Web.config 파일에서 새 데이터베이스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="dae4e-129">OrdersContext.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="dae4e-130">생성자는 데이터베이스 연결 문자열의 이름을 지정 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="dae4e-131">이 이름은 Web.config에 추가 된 연결 문자열을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="dae4e-132">`OrdersContext` 클래스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="dae4e-133">A **DbSet** 쿼리할 수 있는 엔터티 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="dae4e-134">에 대 한 전체 목록은 다음과 같습니다는 `OrdersContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="dae4e-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="dae4e-135">`AdminController` 클래스 기본 CRUD 기능 구현 하는 5 개의 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="dae4e-136">각 메서드는 클라이언트가 호출할 수 있는 URI에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="dae4e-137">컨트롤러 메서드</span><span class="sxs-lookup"><span data-stu-id="dae4e-137">Controller Method</span></span> | <span data-ttu-id="dae4e-138">설명</span><span class="sxs-lookup"><span data-stu-id="dae4e-138">Description</span></span> | <span data-ttu-id="dae4e-139">URI</span><span class="sxs-lookup"><span data-stu-id="dae4e-139">URI</span></span> | <span data-ttu-id="dae4e-140">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="dae4e-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dae4e-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="dae4e-141">GetProducts</span></span> | <span data-ttu-id="dae4e-142">모든 제품을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-142">Gets all products.</span></span> | <span data-ttu-id="dae4e-143">api/제품</span><span class="sxs-lookup"><span data-stu-id="dae4e-143">api/products</span></span> | <span data-ttu-id="dae4e-144">가져오기</span><span class="sxs-lookup"><span data-stu-id="dae4e-144">GET</span></span> |
| <span data-ttu-id="dae4e-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="dae4e-145">GetProduct</span></span> | <span data-ttu-id="dae4e-146">제품을 id를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-146">Finds a product by ID.</span></span> | <span data-ttu-id="dae4e-147">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dae4e-147">api/products/*id*</span></span> | <span data-ttu-id="dae4e-148">가져오기</span><span class="sxs-lookup"><span data-stu-id="dae4e-148">GET</span></span> |
| <span data-ttu-id="dae4e-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="dae4e-149">PutProduct</span></span> | <span data-ttu-id="dae4e-150">제품을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-150">Updates a product.</span></span> | <span data-ttu-id="dae4e-151">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dae4e-151">api/products/*id*</span></span> | <span data-ttu-id="dae4e-152">PUT</span><span class="sxs-lookup"><span data-stu-id="dae4e-152">PUT</span></span> |
| <span data-ttu-id="dae4e-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="dae4e-153">PostProduct</span></span> | <span data-ttu-id="dae4e-154">새 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-154">Creates a new product.</span></span> | <span data-ttu-id="dae4e-155">api/제품</span><span class="sxs-lookup"><span data-stu-id="dae4e-155">api/products</span></span> | <span data-ttu-id="dae4e-156">올리기</span><span class="sxs-lookup"><span data-stu-id="dae4e-156">POST</span></span> |
| <span data-ttu-id="dae4e-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="dae4e-157">DeleteProduct</span></span> | <span data-ttu-id="dae4e-158">제품을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-158">Deletes a product.</span></span> | <span data-ttu-id="dae4e-159">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dae4e-159">api/products/*id*</span></span> | <span data-ttu-id="dae4e-160">Delete</span><span class="sxs-lookup"><span data-stu-id="dae4e-160">DELETE</span></span> |

<span data-ttu-id="dae4e-161">각 메서드를 호출 `OrdersContext` 데이터베이스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="dae4e-162">컬렉션 (PUT, POST 및 DELETE)을 수정 하는 메서드의 호출 `db.SaveChanges` 데이터베이스로 변경 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="dae4e-163">컨트롤러는 HTTP 요청에 따라 생성 및 메서드 반환 되기 전에 변경 내용을 유지 하는 데 필요한 이므로 다음 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="dae4e-164">데이터베이스 이니셜라이저를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-164">Add a Database Initializer</span></span>

<span data-ttu-id="dae4e-165">Entity Framework에는 시작 시 데이터베이스를 채우고 모델 변경 될 때마다 데이터베이스를 자동으로 다시 사용 하면 멋진 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="dae4e-166">이 기능은 모델을 변경 하는 경우에 일부 테스트 데이터를 항상 있기 때문에 개발 하는 동안 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="dae4e-167">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 라는 새 클래스를 만듭니다 `OrdersContextInitializer`합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="dae4e-168">다음 구현에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="dae4e-169">상속 하 여는 **DropCreateDatabaseIfModelChanges** 클래스를 Entity Framework 모델 클래스 수정 될 때마다 데이터베이스를 삭제 하도록 지시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="dae4e-170">Entity Framework (만들거나 다시) 데이터베이스를 호출 합니다 **시드** 메서드는 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="dae4e-171">사용 된 **시드** 일부 예제에서는 제품 및 예제 주문을 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="dae4e-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="dae4e-172">테스트를 위해이 기능은 유용 하지만 사용 하지 않는 합니다 **DropCreateDatabaseIfModelChanges** 모델 클래스 변경 되 면 데이터를 손실 될 수 있으므로 프로덕션, 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="dae4e-173">다음으로, Global.asax를 열고 다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:</span><span class="sxs-lookup"><span data-stu-id="dae4e-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="dae4e-174">컨트롤러에 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="dae4e-174">Send a Request to the Controller</span></span>

<span data-ttu-id="dae4e-175">이 시점에서 클라이언트 코드를 작성 하지 않은 것 이지만 웹 디버깅 하는 HTTP 또는 웹 브라우저를 사용 하 여 API와 같은 도구를 호출할 수 있습니다 [Fiddler](http://www.fiddler2.com/fiddler2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="dae4e-176">Visual Studio에서 f5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="dae4e-177">웹 브라우저가 열립니다 `http://localhost:*portnum*/`, 여기서 *portnum* 일부 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="dae4e-178">HTTP 요청을 보내는 "`http://localhost:*portnum*/api/admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="dae4e-179">Entify 프레임 워크를 만들고 데이터베이스를 시드하고 해야 하기 때문에 첫 번째 요청을 완료 하려면 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-179">The first request may be slow to complete, because Entify Framework needs to create and seed the database.</span></span> <span data-ttu-id="dae4e-180">응답에 다음과 비슷한 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="dae4e-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="dae4e-181">[이전](using-web-api-with-entity-framework-part-2.md)
> [다음](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="dae4e-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
