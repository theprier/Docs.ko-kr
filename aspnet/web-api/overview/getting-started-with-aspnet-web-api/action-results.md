---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: "Web API 2의에서 동작으로 인해 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/03/2014
ms.topic: article
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: d0db5c6d45020861d7295ab1db989caee525fff9
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="action-results-in-web-api-2"></a><span data-ttu-id="aedd0-102">Web API 2의에서 작업 결과</span><span class="sxs-lookup"><span data-stu-id="aedd0-102">Action Results in Web API 2</span></span>
====================
<span data-ttu-id="aedd0-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="aedd0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="aedd0-104">이 항목에서는 ASP.NET Web API HTTP 응답 메시지에 컨트롤러 작업에서 반환 값을 변환 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="aedd0-105">Web API 컨트롤러 작업에는 다음 중 하나를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="aedd0-106">void</span><span class="sxs-lookup"><span data-stu-id="aedd0-106">void</span></span>
2. <span data-ttu-id="aedd0-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="aedd0-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="aedd0-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="aedd0-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="aedd0-109">다른 일부 형식</span><span class="sxs-lookup"><span data-stu-id="aedd0-109">Some other type</span></span>

<span data-ttu-id="aedd0-110">에 따라 다음 중이 반환, 웹 API는 HTTP 응답을 만드는 다른 메커니즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="aedd0-111">반환 형식</span><span class="sxs-lookup"><span data-stu-id="aedd0-111">Return type</span></span> | <span data-ttu-id="aedd0-112">웹 API 응답을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="aedd0-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="aedd0-113">void</span><span class="sxs-lookup"><span data-stu-id="aedd0-113">void</span></span> | <span data-ttu-id="aedd0-114">빈 204 (콘텐츠 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="aedd0-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="aedd0-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="aedd0-116">직접 HTTP 응답 메시지를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="aedd0-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="aedd0-117">**IHttpActionResult**</span></span> | <span data-ttu-id="aedd0-118">호출 **ExecuteAsync** 만들려는 **HttpResponseMessage**, HTTP 응답 메시지를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="aedd0-119">다른 유형</span><span class="sxs-lookup"><span data-stu-id="aedd0-119">Other type</span></span> | <span data-ttu-id="aedd0-120">Serialize 된 반환 값은 고 응답 본문에 쓰기 200 (정상)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="aedd0-121">이 항목의 나머지 부분에서 자세히 각 옵션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="aedd0-122">void</span><span class="sxs-lookup"><span data-stu-id="aedd0-122">void</span></span>

<span data-ttu-id="aedd0-123">반환 형식이 `void`, Web API에서 빈 HTTP 응답 상태 코드 204 (콘텐츠 없음)와 함께 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="aedd0-124">예제에서는 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="aedd0-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="aedd0-125">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="aedd0-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="aedd0-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="aedd0-126">HttpResponseMessage</span></span>

<span data-ttu-id="aedd0-127">작업에서 반환 하는 경우는 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), 웹 API 변환 반환 값은 HTTP 응답 메시지에 직접 속성을 사용 하는 **HttpResponseMessage** 을 채우기 위해 개체는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="aedd0-128">이 옵션을 많이 응답 메시지에 대 한 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="aedd0-129">예를 들어 컨트롤러 동작 캐시 제어 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="aedd0-130">응답:</span><span class="sxs-lookup"><span data-stu-id="aedd0-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="aedd0-131">도메인 모델을 전달 하는 경우는 **CreateResponse** 메서드를 사용 하 여 웹 API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 응답 본문에 serialize 된 모델을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="aedd0-132">Web API 요청의 Accept 헤더를 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="aedd0-133">자세한 내용은 참조 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="aedd0-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="aedd0-134">IHttpActionResult</span></span>

<span data-ttu-id="aedd0-135">**IHttpActionResult** 인터페이스 Web API 2에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="aedd0-136">정의 기본적으로 **HttpResponseMessage** 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="aedd0-137">여기의 일부의 이점은 사용 하 여 **IHttpActionResult** 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="aedd0-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="aedd0-138">간소화 [단위 테스트](../testing-and-debugging/unit-testing-controllers-in-web-api.md) 컨트롤러에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="aedd0-139">HTTP 응답을 별도 클래스를 만들기 위한 공통 논리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="aedd0-140">응답 구성의 하위 수준 세부 정보를 숨겨 명료 컨트롤러 동작의 의도를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="aedd0-141">**IHttpActionResult** 메서드 하나가 포함 **ExecuteAsync**, 비동기적으로 만듭니다는 **HttpResponseMessage** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="aedd0-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="aedd0-142">컨트롤러 작업을 반환 하는 경우는 **IHttpActionResult**, 웹 API 호출는 **ExecuteAsync** 만드는 메서드를 한 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="aedd0-143">변환 후의 **HttpResponseMessage** HTTP 응답 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="aedd0-144">다음의 간단한 한 않아도 됨은 **IHttpActionResult** 를 만드는 일반 텍스트 응답:</span><span class="sxs-lookup"><span data-stu-id="aedd0-144">Here is a simple implementaton of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="aedd0-145">예제에서는 컨트롤러 동작:</span><span class="sxs-lookup"><span data-stu-id="aedd0-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="aedd0-146">응답:</span><span class="sxs-lookup"><span data-stu-id="aedd0-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="aedd0-147">사용할 더 자주는 **IHttpActionResult** 에 정의 된 구현은  **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)**  네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-147">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="aedd0-148">**ApiController** 클래스는 이러한 기본 제공 작업 결과 반환 하는 도우미 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="aedd0-149">다음 예제에서 요청은 기존 제품 ID와 일치 하지 않으면 컨트롤러 호출 [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 404 (찾을 수 없음) 응답을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="aedd0-150">그렇지 않으면 컨트롤러 호출 [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), 제품을 포함 하는 200 (OK) 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="aedd0-151">다른 반환 형식</span><span class="sxs-lookup"><span data-stu-id="aedd0-151">Other Return Types</span></span>

<span data-ttu-id="aedd0-152">반환 다른 모든 형식에 대 한 웹 API에 사용 된 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 반환 값을 직렬화 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="aedd0-153">Web API 응답 본문으로 직렬화 된 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="aedd0-154">응답 상태 코드는 200 (정상)입니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="aedd0-155">이 방법의 단점은 예: 404 오류 코드에 직접 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="aedd0-156">Throw 할 수 있습니다는 **HttpResponseException** 오류 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="aedd0-157">자세한 내용은 참조 [ASP.NET Web API의 예외 처리](../error-handling/exception-handling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="aedd0-158">Web API 요청의 Accept 헤더를 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="aedd0-159">자세한 내용은 참조 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aedd0-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="aedd0-160">예제 요청</span><span class="sxs-lookup"><span data-stu-id="aedd0-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="aedd0-161">예제 응답:</span><span class="sxs-lookup"><span data-stu-id="aedd0-161">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
