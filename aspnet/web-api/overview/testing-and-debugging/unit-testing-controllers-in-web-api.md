---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2의에서 단위 테스트 컨트롤러 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 Web API 2의 단위 테스트 컨트롤러에 대 한 몇 가지 특정 기술을 설명 합니다. 이 항목을 읽기 전에 자습서 단위를 읽기만 하는 것이 좋습니다는 중...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7b0d5266757219a05b25fc3d1d4cba8514a4dff7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829870"
---
<a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="31818-104">ASP.NET Web API 2의에서 단위 테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="31818-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="31818-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="31818-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="31818-106">이 항목에서는 Web API 2의 단위 테스트 컨트롤러에 대 한 몇 가지 특정 기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="31818-107">이 항목을 읽기 전에 하려는 경우 자습서를 읽어 보세요 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), 단위 테스트 프로젝트를 솔루션에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31818-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="31818-108">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="31818-108">Software versions used in the tutorial</span></span>
> 
> - [<span data-ttu-id="31818-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="31818-109">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="31818-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="31818-110">Web API 2</span></span>
> - <span data-ttu-id="31818-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="31818-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="31818-112">Moq를 사용 하지만 동일한 개념 모든 모의 프레임 워크에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31818-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="31818-113">Moq 4.5.30 (이상) Visual Studio 2017, Roslyn 및.NET 4.5 이상 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="31818-114">단위 테스트에서 일반적인 패턴은 &quot;정렬 act assert&quot;:</span><span class="sxs-lookup"><span data-stu-id="31818-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="31818-115">설정 테스트를 실행 하려면 모든 필수 구성 요소를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="31818-116">Act: 테스트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-116">Act: Perform the test.</span></span>
- <span data-ttu-id="31818-117">Assert: 테스트가 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="31818-118">정렬 단계에는 자주 mock를 사용 하거나 스텁 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="31818-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="31818-119">한 가지 테스트에서 테스트 포커스가 하므로 종속성 수가 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31818-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="31818-120">Web API 컨트롤러에서 단위 테스트를 해야 하는 몇 가지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="31818-121">작업 응답의 올바른 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="31818-122">잘못 된 매개 변수가 올바른 오류 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="31818-123">리포지토리 또는 서비스 계층에서 올바른 메서드를 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="31818-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="31818-124">응답 도메인 모델에 포함 된 경우에 모델 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="31818-125">다음은 몇 가지 일반 작업을 테스트 하려면 하지만 세부 정보 컨트롤러 구현에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="31818-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="31818-126">컨트롤러 작업 반환 하는지 여부를 크게 향상 될 수 하는 특히 **HttpResponseMessage** 하거나 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="31818-127">이러한 결과 형식에 대 한 자세한 내용은 참조 하세요. [Web Api 2에서 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="31818-128">HttpResponseMessage를 반환 하는 테스트 작업</span><span class="sxs-lookup"><span data-stu-id="31818-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="31818-129">한 예로 컨트롤러 작업 반환 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="31818-130">컨트롤러 삽입에 종속성 주입 사용을 `IProductRepository`입니다.</span><span class="sxs-lookup"><span data-stu-id="31818-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="31818-131">사용 컨트롤러 더 테스트할 수 있으므로 모의 리포지토리를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="31818-132">다음 단위 테스트를 확인 합니다 `Get` 메서드 쓰기를 `Product` 응답 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="31818-133">가정 `repository` mock는 `IProductRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="31818-134">설정 해야 **요청** 하 고 **구성** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="31818-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="31818-135">사용 하 여 테스트에 실패 하는 고, 그렇지는 **ArgumentNullException** 하거나 **InvalidOperationException**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="31818-136">테스트 링크 생성</span><span class="sxs-lookup"><span data-stu-id="31818-136">Testing Link Generation</span></span>

<span data-ttu-id="31818-137">합니다 `Post` 메서드 호출 **UrlHelper.Link** 응답에 링크를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="31818-138">이 단위 테스트에서 약간 더 많은 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="31818-139">합니다 **UrlHelper** 클래스 테스트에 대 한 값을 설정 해야 하므로 요청 URL 및 경로 데이터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="31818-140">또 다른 옵션은 stub 또는 mock **UrlHelper**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="31818-141">이 방법의 기본 값을 바꿔야 [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) 고정된 값을 반환 하는 mock 또는 스텁 버전을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="31818-142">사용 하 여 테스트를 다시 작성해 보겠습니다 합니다 [Moq](https://github.com/Moq) 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="31818-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="31818-143">설치는 `Moq` 테스트 프로젝트에서 NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="31818-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="31818-144">이 버전에서는 필요가 경로 데이터를 설정 하기 때문에 mock **UrlHelper** 상수 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>


## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="31818-145">IHttpActionResult 반환 하는 테스트 작업</span><span class="sxs-lookup"><span data-stu-id="31818-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="31818-146">Web API 2 컨트롤러 작업을 반환할 수 있습니다 **IHttpActionResult**에 비슷합니다 **ActionResult** ASP.NET MVC에서.</span><span class="sxs-lookup"><span data-stu-id="31818-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="31818-147">합니다 **IHttpActionResult** 인터페이스는 HTTP 응답을 만들기 위한 명령 패턴을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="31818-148">컨트롤러 응답을 직접 만드는 대신 반환 된 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="31818-149">파이프라인을 호출 하는 나중에 **IHttpActionResult** 응답을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="31818-150">이 접근 방식을 쉽게 단위 테스트 작성에 필요한 설정의 많은 건너뛸 수 있으므로 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="31818-151">같습니다.는 예제 컨트롤러 작업 반환 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="31818-152">이 예제를 사용 하 여 몇 가지 일반적인 패턴을 보여 줍니다 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="31818-153">살펴보겠습니다 어떻게 단위를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="31818-154">작업 응답 본문이 포함 된 200 (정상)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="31818-155">합니다 `Get` 메서드 호출 `Ok(product)` 제품 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31818-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="31818-156">단위 테스트에서 반환 형식 인지 확인 **OkNegotiatedContentResult** 및 반환 된 제품에는 올바른 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="31818-157">단위 테스트는 작업 결과 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="31818-158">작업 결과 HTTP 응답을를 올바르게 만드는 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31818-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="31818-159">(이유는 Web API 프레임 워크에는 자체 단위 테스트가!)</span><span class="sxs-lookup"><span data-stu-id="31818-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="31818-160">작업 404 (찾을 수 없음)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="31818-161">합니다 `Get` 메서드 호출 `NotFound()` 제품 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="31818-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="31818-162">이 경우에 대 한 단위 테스트에 검사 반환 형식이 **NotFoundResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="31818-163">작업 응답 본문 없이 200 (정상)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="31818-164">합니다 `Delete` 메서드 호출 `Ok()` 빈 HTTP 200 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="31818-165">단위 테스트는 이전 예제와 같이 반환 형식으로이 경우 확인 **OkResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="31818-166">작업 위치 헤더를 사용 하 여 201 (만들어짐)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="31818-167">합니다 `Post` 메서드 호출 `CreatedAtRoute` Location 헤더의 URI 사용 하 여 HTTP 201 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="31818-168">단위 테스트를 작업에 올바른 라우팅 값 설정 함을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="31818-169">작업 응답 본문이 포함 된 다른 2xx를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="31818-170">합니다 `Put` 메서드 호출 `Content` 응답 본문과 함께 HTTP 202 (수락 됨) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="31818-171">이 경우 200 (정상)를 반환 하도록 유사 하지만 단위 테스트 상태 코드를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31818-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="31818-172">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="31818-172">Additional Resources</span></span>

- [<span data-ttu-id="31818-173">Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="31818-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="31818-174">[ASP.NET 웹 API 서비스에 대 한 테스트를 작성](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaoui 블로그 게시물).</span><span class="sxs-lookup"><span data-stu-id="31818-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="31818-175">경로 디버거를 사용 하 여 ASP.NET Web API 디버깅</span><span class="sxs-lookup"><span data-stu-id="31818-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
