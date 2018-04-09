---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET 클라이언트 (C#)에서 Web API를 호출 합니다. | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/24/2017
ms.topic: article
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: a243eeb982ba581e237263c4e31e130d634aff0e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="27cba-102">.NET 클라이언트 (C#)에서 Web API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-102">Call a Web API From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="27cba-103">여 [Mike Wasson](https://github.com/MikeWasson) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="27cba-103">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="27cba-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-104">Download Completed Project</span></span>](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)

<span data-ttu-id="27cba-105">.NET 응용 프로그램에서 web API를 호출 하는 방법을 보여 주는이 자습서를 사용 하 여 [System.Net.Http.HttpClient 합니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="27cba-105">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="27cba-106">이 자습서에서는 다음 web API를 사용 하는 클라이언트 응용 프로그램 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-106">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="27cba-107">작업</span><span class="sxs-lookup"><span data-stu-id="27cba-107">Action</span></span> | <span data-ttu-id="27cba-108">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="27cba-108">HTTP method</span></span> | <span data-ttu-id="27cba-109">상대 URI</span><span class="sxs-lookup"><span data-stu-id="27cba-109">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27cba-110">제품을 ID 별로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-110">Get a product by ID</span></span> | <span data-ttu-id="27cba-111">가져오기</span><span class="sxs-lookup"><span data-stu-id="27cba-111">GET</span></span> | <span data-ttu-id="27cba-112">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="27cba-112">/api/products/*id*</span></span> |
| <span data-ttu-id="27cba-113">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="27cba-113">Create a new product</span></span> | <span data-ttu-id="27cba-114">올리기</span><span class="sxs-lookup"><span data-stu-id="27cba-114">POST</span></span> | <span data-ttu-id="27cba-115">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="27cba-115">/api/products</span></span> |
| <span data-ttu-id="27cba-116">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="27cba-116">Update a product</span></span> | <span data-ttu-id="27cba-117">PUT</span><span class="sxs-lookup"><span data-stu-id="27cba-117">PUT</span></span> | <span data-ttu-id="27cba-118">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="27cba-118">/api/products/*id*</span></span> |
| <span data-ttu-id="27cba-119">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="27cba-119">Delete a product</span></span> | <span data-ttu-id="27cba-120">Delete</span><span class="sxs-lookup"><span data-stu-id="27cba-120">DELETE</span></span> | <span data-ttu-id="27cba-121">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="27cba-121">/api/products/*id*</span></span> |

<span data-ttu-id="27cba-122">ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 참조 [CRUD 작업을 지원 합니다. 해당 웹 API를 만드는](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-122">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="27cba-123">간단한 설명을 위해이 자습서에서는 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-123">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="27cba-124">**HttpClient** Windows Phone 및 Windows 스토어 앱 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-124">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="27cba-125">자세한 내용은 참조 [여러 플랫폼 이식 가능한 라이브러리 사용에 대 한 웹 API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="27cba-125">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="27cba-126">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="27cba-126">Create the Console Application</span></span>

<span data-ttu-id="27cba-127">Visual Studio에서 명명 된 새 Windows 콘솔 앱을 만듭니다 **HttpClientSample** 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-127">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="27cba-128">위의 코드는 완전 한 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-128">The preceding code is the complete client app.</span></span>

<span data-ttu-id="27cba-129">`RunAsync` 완료 될 때까지 블록 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-129">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="27cba-130">대부분 **HttpClient** 네트워크 I/O를 수행 하기 때문에 메서드는 비동기 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-130">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="27cba-131">비동기 작업을 모두에서 수행 된 `RunAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-131">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="27cba-132">일반적으로 응용 프로그램 주 스레드를 차단 하지 않습니다 되지만이 응용 프로그램 상호 작용을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-132">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="27cba-133">웹 API 클라이언트 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="27cba-133">Install the Web API Client Libraries</span></span>

<span data-ttu-id="27cba-134">NuGet 패키지 관리자를 사용 하 여 Web API Client Libraries 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-134">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="27cba-135">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-135">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="27cba-136">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-136">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="27cba-137">위의 명령은 프로젝트에 다음과 같은 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-137">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="27cba-138">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="27cba-138">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="27cba-139">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="27cba-139">Newtonsoft.Json</span></span>

<span data-ttu-id="27cba-140">Json.NET은.NET을 위한 인기 있는 고성능 JSON 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-140">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="27cba-141">모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-141">Add a Model Class</span></span>

<span data-ttu-id="27cba-142">검사는 `Product` 클래스:</span><span class="sxs-lookup"><span data-stu-id="27cba-142">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="27cba-143">이 클래스는 web API에서 사용 하는 데이터 모델을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-143">This class matches the data model used by the web API.</span></span> <span data-ttu-id="27cba-144">응용 프로그램에서 사용할 수 **HttpClient** 읽을 수는 `Product` HTTP 응답 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-144">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="27cba-145">응용 프로그램을 deserialization 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-145">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="27cba-146">만들기 및 HttpClient를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-146">Create and Initialize HttpClient</span></span>

<span data-ttu-id="27cba-147">정적 검사 **HttpClient** 속성:</span><span class="sxs-lookup"><span data-stu-id="27cba-147">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="27cba-148">**HttpClient** 한 번만 인스턴스화할 수 이며 응용 프로그램의 수명 내내 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-148">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="27cba-149">다음 조건이 발생할 수 있습니다 **SocketException** 오류:</span><span class="sxs-lookup"><span data-stu-id="27cba-149">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="27cba-150">새 **HttpClient** 요청당 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="27cba-150">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="27cba-151">서버 로드가 많은 상황입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-151">Server under heavy load.</span></span>

<span data-ttu-id="27cba-152">새 **HttpClient** 요청당 인스턴스 사용 가능한 소켓 빠른 속도로 소모 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-152">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="27cba-153">다음 코드를 초기화 하는 **HttpClient** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="27cba-153">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="27cba-154">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="27cba-154">The preceding code:</span></span>

* <span data-ttu-id="27cba-155">HTTP 요청에 대 한 기본 URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-155">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="27cba-156">서버 응용 프로그램에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-156">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="27cba-157">응용 프로그램 서버 응용 프로그램에 대 한 포트를 사용 하지 않으면 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-157">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="27cba-158">Accept 헤더가 "application/json"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-158">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="27cba-159">이 헤더를 설정 합니다. JSON 형식의 데이터를 보낼 서버를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-159">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="27cba-160">리소스를 검색 하는 GET 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="27cba-160">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="27cba-161">다음 코드는 제품에 대 한 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-161">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="27cba-162">**GetAsync** 메서드 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-162">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="27cba-163">메서드가 완료 될 때 반환 된 **HttpResponseMessage** HTTP 응답이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-163">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="27cba-164">응답에 상태 코드가 성공 코드 이면 응답 본문에는 제품의 JSON 표현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-164">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="27cba-165">호출 **ReadAsAsync** JSON 페이로드를 deserialize 하는 데는 `Product` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="27cba-165">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="27cba-166">**ReadAsAsync** 응답 본문은 임의로 큰 수 있기 때문에 메서드는 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-166">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="27cba-167">**HttpClient** HTTP 응답에 오류 코드가 포함 되어 있으면 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-167">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="27cba-168">대신,는 **IsSuccessStatusCode** 속성은 **false** 면 상태는 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-168">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="27cba-169">HTTP 오류 코드 예외를 처리 하는 것을 선호 하는 경우 호출 [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 응답 개체에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-169">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="27cba-170">`EnsureSuccessStatusCode` 상태 코드 200 범위를 벗어나는 경우 예외를 throw&ndash;299 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-170">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="27cba-171">**HttpClient** 다른 이유로 예외를 throw 할 수 &mdash; 요청 시간이 초과 하는 경우 등입니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-171">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="27cba-172">미디어 유형 포맷터를 역직렬화</span><span class="sxs-lookup"><span data-stu-id="27cba-172">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="27cba-173">때 **ReadAsAsync** 라고 매개 변수 없이 사용 하 여 일련의 기본 *미디어 포맷터* 응답 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-173">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="27cba-174">기본 포맷터 JSON, XML 및 양식 url로 인코딩된 데이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-174">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="27cba-175">기본 포맷터를 사용 하는 대신에 포맷터의 목록을 제공할 수 있습니다는 **ReadAsAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="27cba-175">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="27cba-176">포맷터의 목록을 사용 하 여 하는 것은 사용자 지정 미디어 유형 포맷터를가 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-176">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="27cba-177">자세한 내용은 참조 [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="27cba-177">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="27cba-178">리소스를 만드는 POST 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="27cba-178">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="27cba-179">다음 코드를 포함 하 여 POST 요청을 보냅니다는 `Product` JSON 형식의 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="27cba-179">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="27cba-180">**PostAsJsonAsync** 메서드:</span><span class="sxs-lookup"><span data-stu-id="27cba-180">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="27cba-181">JSON으로 개체를 serialize합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-181">Serializes an object to JSON.</span></span>
* <span data-ttu-id="27cba-182">POST 요청에 JSON 페이로드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-182">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="27cba-183">요청이 성공 하면:</span><span class="sxs-lookup"><span data-stu-id="27cba-183">If the request succeeds:</span></span>

* <span data-ttu-id="27cba-184">201 (만들어짐) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-184">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="27cba-185">응답의 위치 헤더에서 만든된 리소스의 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-185">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="27cba-186">리소스를 업데이트 하는 PUT 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="27cba-186">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="27cba-187">다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-187">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="27cba-188">**PutAsJsonAsync** 처럼 사용할 수 있는 방법 **PostAsJsonAsync**제외 하 고 게시 하는 대신 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-188">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="27cba-189">리소스를 삭제 하는 DELETE 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="27cba-189">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="27cba-190">다음 코드는 제품을 삭제 하는 DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-190">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="27cba-191">GET, 처럼 DELETE 요청은 요청 본문이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-191">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="27cba-192">DELETE로 JSON 또는 XML 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-192">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="27cba-193">예제 테스트</span><span class="sxs-lookup"><span data-stu-id="27cba-193">Test the sample</span></span>

<span data-ttu-id="27cba-194">클라이언트 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-194">To test the client app:</span></span>

1. <span data-ttu-id="27cba-195">[다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 및 서버 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-195">[Download](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="27cba-196">[지침을 다운로드하세요](https://docs.microsoft.com/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="27cba-196">[Download instructions](https://docs.microsoft.com/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="27cba-197">서버 응용 프로그램 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-197">Verify the server app is working.</span></span> <span data-ttu-id="27cba-198">Exaxmple에 대 한 `http://localhost:64195/api/products` 제품 목록이 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-198">For exaxmple, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="27cba-199">HTTP 요청에 대 한 기본 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-199">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="27cba-200">서버 응용 프로그램에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-200">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="27cba-201">클라이언트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-201">Run the client app.</span></span> <span data-ttu-id="27cba-202">다음 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27cba-202">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
