---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 양식 urlencoded 데이터 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/15/2012
ms.topic: article
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 24410c92df828d4aaaa3b91dd3e9fa14575fd300
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399872"
---
<a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="9c04f-102">ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 양식 urlencoded 데이터</span><span class="sxs-lookup"><span data-stu-id="9c04f-102">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>
====================
<span data-ttu-id="9c04f-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9c04f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="9c04f-104">1 부: 양식 urlencoded 데이터</span><span class="sxs-lookup"><span data-stu-id="9c04f-104">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="9c04f-105">이 문서에서는 Web API 컨트롤러에 양식 urlencoded 데이터를 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-105">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="9c04f-106">HTML 폼의 개요</span><span class="sxs-lookup"><span data-stu-id="9c04f-106">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="9c04f-107">보내는 복합 형식</span><span class="sxs-lookup"><span data-stu-id="9c04f-107">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="9c04f-108">AJAX 통해 양식 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="9c04f-108">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="9c04f-109">보내는 단순 형식</span><span class="sxs-lookup"><span data-stu-id="9c04f-109">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="9c04f-110">[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-110">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="9c04f-111">HTML 폼의 개요</span><span class="sxs-lookup"><span data-stu-id="9c04f-111">Overview of HTML Forms</span></span>

<span data-ttu-id="9c04f-112">HTML 양식 사용 하 여 GET 또는 게시 서버로 데이터를 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-112">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="9c04f-113">**메서드** 특성을 **폼** HTTP 메서드를 제공 하는 요소:</span><span class="sxs-lookup"><span data-stu-id="9c04f-113">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="9c04f-114">기본 메서드는 GET입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-114">The default method is GET.</span></span> <span data-ttu-id="9c04f-115">양식을 사용 하는 경우를 가져오려면 데이터를 URI 쿼리 문자열로 인코딩된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-115">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="9c04f-116">폼 POST를 사용 하는 경우 양식 데이터가 요청 본문에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-116">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="9c04f-117">게시 된 데이터에 대 한 합니다 **enctype** 특성 요청 본문의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-117">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="9c04f-118">enctype</span><span class="sxs-lookup"><span data-stu-id="9c04f-118">enctype</span></span> | <span data-ttu-id="9c04f-119">설명</span><span class="sxs-lookup"><span data-stu-id="9c04f-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c04f-120">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="9c04f-120">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="9c04f-121">양식 데이터는 URI 쿼리 문자열로 비슷합니다 이름/값 쌍으로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-121">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="9c04f-122">게시물에 대 한 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-122">This is the default format for POST.</span></span> |
| <span data-ttu-id="9c04f-123">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="9c04f-123">multipart/form-data</span></span> | <span data-ttu-id="9c04f-124">양식 데이터는 다중 파트 MIME 메시지를로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-124">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="9c04f-125">서버에 파일을 업로드 하는 경우이 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-125">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="9c04f-126">이 기사의 1 부 x-www-형식-urlencoded 형식에 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-126">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="9c04f-127">[2 부](sending-html-form-data-part-2.md) 다중 파트 MIME에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-127">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="9c04f-128">보내는 복합 형식</span><span class="sxs-lookup"><span data-stu-id="9c04f-128">Sending Complex Types</span></span>

<span data-ttu-id="9c04f-129">일반적으로 여러 폼 컨트롤에서 가져온 값으로 구성 된 복합 형식에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-129">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="9c04f-130">상태 업데이트를 나타내는 다음 모델을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-130">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="9c04f-131">다음은 허용 하는 Web API 컨트롤러는 `Update` POST 통해 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-131">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="9c04f-132">이 컨트롤러를 사용 하 여 [동작 기반 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)이므로 경로 템플릿은 &quot;api / {컨트롤러} / {action} / {id}&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-132">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="9c04f-133">클라이언트 데이터를 게시할 예정 &quot;/api/updates/complex&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-133">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="9c04f-134">이제 상태 업데이트를 제출 하는 사용자에 대 한 HTML 폼을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-134">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="9c04f-135">에 **작업** 양식의 특성이 컨트롤러 작업의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-135">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="9c04f-136">폼에 입력 한 일부 값으로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-136">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="9c04f-137">사용자가 제출 하는 경우 브라우저는 HTTP 요청을 유사한 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-137">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="9c04f-138">요청 본문은 이름/값 쌍 형식으로 폼 데이터를 포함 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-138">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="9c04f-139">웹 API는 자동으로 이름/값 쌍의 인스턴스로 변환 합니다 `Update` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-139">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="9c04f-140">AJAX 통해 양식 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="9c04f-140">Sending Form Data via AJAX</span></span>

<span data-ttu-id="9c04f-141">사용자가 폼을 제출 하면 브라우저는 현재 페이지 밖으로 이동 하 고 응답 메시지의 본문을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-141">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="9c04f-142">이런 경우 확인 응답은 HTML 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-142">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="9c04f-143">하지만 Web API 사용 응답 본문은 일반적으로 비어 있거나 JSON과 같은 구조화 된 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-143">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="9c04f-144">이 경우 편이 보낼 AJAX를 사용 하 여 폼 데이터 요청, 페이지 응답을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-144">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="9c04f-145">다음 코드에는 jQuery를 사용 하 여 폼 데이터를 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-145">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="9c04f-146">JQuery **제출** 함수는 새 함수를 사용 하 여 form action을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-146">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="9c04f-147">이 제출 단추의 기본 동작을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-147">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="9c04f-148">합니다 **serialize** 함수 이름/값 쌍에 양식 데이터를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-148">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="9c04f-149">서버에 폼 데이터를 보내도록 호출 `$.post()`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-149">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="9c04f-150">요청이 완료 되 면 합니다 `.success()` 또는 `.error()` 처리기는 사용자에 게 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-150">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="9c04f-151">보내는 단순 형식</span><span class="sxs-lookup"><span data-stu-id="9c04f-151">Sending Simple Types</span></span>

<span data-ttu-id="9c04f-152">이전 섹션에서는 Web API 모델 클래스의 인스턴스로 deserialize 하는 복합 형식을 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-152">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="9c04f-153">또한 문자열 등의 단순 형식에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-153">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="9c04f-154">단순 형식을 보내기 전에 대신 복합 형식의 값을 배치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-154">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="9c04f-155">이 서버 쪽에서 모델 유효성 검사의 이점을 제공 하며, 쉽게 모델을 확장 하는 데 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="9c04f-155">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="9c04f-156">단순 형식을 전송 하는 기본 단계는 동일 하지만 두 가지 미묘한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-156">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="9c04f-157">첫째, 컨트롤러에서 데코레이트해야 매개 변수 이름 앞에 **FromBody** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-157">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="9c04f-158">기본적으로 웹 API는 요청 URI에서에서 단순 형식을 가져오려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-158">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="9c04f-159">합니다 **FromBody** 특성은 요청 본문에서 값을 읽을 수 있는 Web API에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-159">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="9c04f-160">웹 API 응답 본문을 읽습니다 많아야 한 번만 매개 변수는 작업 중 하나는 요청 본문에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-160">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="9c04f-161">요청 본문에서 여러 값을 얻으려면 해야 할 경우에 복합 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-161">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="9c04f-162">둘째, 클라이언트는 다음 형식으로 값을 보낼 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-162">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="9c04f-163">특히, 이름/값 쌍의 이름 부분을 단순 형식에 대 한 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-163">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="9c04f-164">일부 브라우저는이 HTML 폼에 대 한 지원 하지만 다음과 같이 스크립트에서이 형식의 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-164">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="9c04f-165">폼에는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-165">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="9c04f-166">및 양식 값을 제출 하는 스크립트 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-166">And here is the script to submit the form value.</span></span> <span data-ttu-id="9c04f-167">이전 스크립트에서 유일한 차이점은에 전달 된 인수를 **게시물** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-167">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="9c04f-168">단순 형식의 배열을 보낼 동일한 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c04f-168">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="9c04f-169">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9c04f-169">Additional Resources</span></span>

[<span data-ttu-id="9c04f-170">2 부: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="9c04f-170">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
