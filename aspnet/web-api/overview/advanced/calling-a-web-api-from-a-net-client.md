---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET 클라이언트 (C#)에서 Web API 호출 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 11/24/2017
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: be237bee43bc5e32939cb0b3e0948fd8b35bd1eb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832311"
---
<a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="dc942-102">.NET 클라이언트 (C#)에서 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="dc942-102">Call a Web API From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="dc942-103">하 여 [Mike Wasson](https://github.com/MikeWasson) 고 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dc942-103">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="dc942-104">[완료 된 프로젝트 다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-104">[Download Completed Project](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="dc942-105">[지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="dc942-105">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="dc942-106">이 자습서에서는.NET 응용 프로그램, web API를 호출 하는 방법을 보여 줍니다.를 사용 하 여 [System.Net.Http.HttpClient 합니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="dc942-106">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="dc942-107">이 자습서에서는 다음 웹 API를 사용 하는 클라이언트 앱을 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-107">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="dc942-108">작업</span><span class="sxs-lookup"><span data-stu-id="dc942-108">Action</span></span> | <span data-ttu-id="dc942-109">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="dc942-109">HTTP method</span></span> | <span data-ttu-id="dc942-110">상대 URI</span><span class="sxs-lookup"><span data-stu-id="dc942-110">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc942-111">제품 ID 별로 가져오기</span><span class="sxs-lookup"><span data-stu-id="dc942-111">Get a product by ID</span></span> | <span data-ttu-id="dc942-112">가져오기</span><span class="sxs-lookup"><span data-stu-id="dc942-112">GET</span></span> | <span data-ttu-id="dc942-113">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dc942-113">/api/products/*id*</span></span> |
| <span data-ttu-id="dc942-114">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="dc942-114">Create a new product</span></span> | <span data-ttu-id="dc942-115">올리기</span><span class="sxs-lookup"><span data-stu-id="dc942-115">POST</span></span> | <span data-ttu-id="dc942-116">api 제품</span><span class="sxs-lookup"><span data-stu-id="dc942-116">/api/products</span></span> |
| <span data-ttu-id="dc942-117">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="dc942-117">Update a product</span></span> | <span data-ttu-id="dc942-118">PUT</span><span class="sxs-lookup"><span data-stu-id="dc942-118">PUT</span></span> | <span data-ttu-id="dc942-119">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dc942-119">/api/products/*id*</span></span> |
| <span data-ttu-id="dc942-120">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="dc942-120">Delete a product</span></span> | <span data-ttu-id="dc942-121">Delete</span><span class="sxs-lookup"><span data-stu-id="dc942-121">DELETE</span></span> | <span data-ttu-id="dc942-122">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="dc942-122">/api/products/*id*</span></span> |

<span data-ttu-id="dc942-123">참조를 ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 [Web API에서는 CRUD 작업을 만드는](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-123">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="dc942-124">간단히 하기 위해이 자습서에서는 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-124">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="dc942-125">**HttpClient** Windows Phone 및 Windows 스토어 앱도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-125">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="dc942-126">자세한 내용은 참조 하세요. [여러 플랫폼 이식 가능한 라이브러리 사용에 대 한 웹 API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="dc942-126">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="dc942-127">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="dc942-127">Create the Console Application</span></span>

<span data-ttu-id="dc942-128">Visual Studio에서 명명 된 새 Windows 콘솔 앱을 만듭니다 **HttpClientSample** 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-128">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="dc942-129">위의 코드는 전체 클라이언트 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-129">The preceding code is the complete client app.</span></span>

<span data-ttu-id="dc942-130">`RunAsync` 실행 및 완료 될 때까지 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-130">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="dc942-131">대부분 **HttpClient** 메서드는 비동기, 네트워크 I/O를 수행 하는 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-131">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="dc942-132">내부에서 수행 하는 비동기 작업을 모두 `RunAsync`입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-132">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="dc942-133">일반적으로 앱 주 스레드를 차단 하지 않습니다 하지만이 앱이 모든 상호 작용을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-133">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="dc942-134">웹 API 클라이언트 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="dc942-134">Install the Web API Client Libraries</span></span>

<span data-ttu-id="dc942-135">NuGet 패키지 관리자를 사용 하 여 웹 API 클라이언트 라이브러리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-135">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="dc942-136">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-136">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="dc942-137">에 콘솔 PMC (패키지 관리자), 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-137">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="dc942-138">위의 명령은 프로젝트에 다음 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-138">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="dc942-139">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="dc942-139">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="dc942-140">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="dc942-140">Newtonsoft.Json</span></span>

<span data-ttu-id="dc942-141">Json.NET은.NET에 대 한 인기 있는 고성능 JSON 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-141">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="dc942-142">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="dc942-142">Add a Model Class</span></span>

<span data-ttu-id="dc942-143">검사는 `Product` 클래스:</span><span class="sxs-lookup"><span data-stu-id="dc942-143">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="dc942-144">이 클래스는 웹 API에 의해 사용 되는 데이터 모델을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-144">This class matches the data model used by the web API.</span></span> <span data-ttu-id="dc942-145">앱에서 사용할 수 있습니다 **HttpClient** 읽을 수는 `Product` HTTP 응답 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-145">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="dc942-146">앱은 deserialization 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-146">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="dc942-147">만들기 및 HttpClient를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-147">Create and Initialize HttpClient</span></span>

<span data-ttu-id="dc942-148">정적 검사 **HttpClient** 속성:</span><span class="sxs-lookup"><span data-stu-id="dc942-148">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="dc942-149">**HttpClient** 한 번 인스턴스화되면 되 고 응용 프로그램의 수명 내내 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-149">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="dc942-150">다음 조건이 발생할 수 있습니다 **SocketException** 오류:</span><span class="sxs-lookup"><span data-stu-id="dc942-150">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="dc942-151">새로 만들 **HttpClient** 요청당 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="dc942-151">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="dc942-152">부하가 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-152">Server under heavy load.</span></span>

<span data-ttu-id="dc942-153">새로 만들 **HttpClient** 요청당 인스턴스는 사용 가능한 소켓 소모 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-153">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="dc942-154">다음 코드는 초기화 된 **HttpClient** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="dc942-154">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="dc942-155">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="dc942-155">The preceding code:</span></span>

* <span data-ttu-id="dc942-156">HTTP 요청에 대 한 기본 URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-156">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="dc942-157">서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-157">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="dc942-158">앱 서버 앱에 대 한 포트를 사용 하지 않으면 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-158">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="dc942-159">Accept 헤더가 "application/json"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-159">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="dc942-160">이 헤더를 설정 합니다. JSON 형식으로 데이터를 보내도록 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-160">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="dc942-161">리소스를 검색에 GET 요청을 보냄</span><span class="sxs-lookup"><span data-stu-id="dc942-161">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="dc942-162">다음 코드는 제품에 대 한 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-162">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="dc942-163">합니다 **GetAsync** 메서드는 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-163">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="dc942-164">메서드가 완료 되 면 반환 된 **HttpResponseMessage** HTTP 응답을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-164">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="dc942-165">응답에 상태 코드가 성공 코드 인 경우 응답 본문에는 제품의 JSON 표현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-165">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="dc942-166">호출 **ReadAsAsync** JSON 페이로드를 deserialize 하는 데는 `Product` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="dc942-166">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="dc942-167">합니다 **ReadAsAsync** 메서드는 응답 본문은 임의로 큰 수 있기 때문에 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-167">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="dc942-168">**HttpClient** HTTP 응답 오류 코드를 포함 하는 경우 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-168">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="dc942-169">대신 합니다 **IsSuccessStatusCode** 속성은 **false** 상태가 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-169">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="dc942-170">HTTP 오류 코드를 예외로 처리 하는 것을 선호 하는 경우 호출 [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 응답 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-170">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="dc942-171">`EnsureSuccessStatusCode` 상태 코드 200 범위를 벗어나는 경우 예외를 throw&ndash;299 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-171">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="dc942-172">사실은 **HttpClient** 다른 이유로 예외를 throw 할 수 있습니다 &mdash; 예를 들어 요청 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-172">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="dc942-173">Deserialize 하는 미디어 유형 포맷터</span><span class="sxs-lookup"><span data-stu-id="dc942-173">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="dc942-174">때 **ReadAsAsync** 라고 일련의 기본 매개 변수 없이 사용 *미디어 포맷터* 응답 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-174">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="dc942-175">기본 포맷터는 JSON, XML 및 양식 url로 인코딩된 데이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-175">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="dc942-176">기본 포맷터를 사용 하는 대신 하는 포맷터의 목록을 제공할 수 있습니다 합니다 **ReadAsAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="dc942-176">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="dc942-177">포맷터 목록을 사용 하 여는 사용자 지정 미디어 유형 포맷터를 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-177">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="dc942-178">자세한 내용은 참조 하세요. [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="dc942-178">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="dc942-179">리소스를 만드는 POST 요청</span><span class="sxs-lookup"><span data-stu-id="dc942-179">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="dc942-180">다음 코드를 포함 하는 POST 요청이 전송 된 `Product` JSON 형식으로 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="dc942-180">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="dc942-181">합니다 **PostAsJsonAsync** 메서드:</span><span class="sxs-lookup"><span data-stu-id="dc942-181">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="dc942-182">Json 개체를 serialize합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-182">Serializes an object to JSON.</span></span>
* <span data-ttu-id="dc942-183">POST 요청에 JSON 페이로드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-183">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="dc942-184">요청이 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-184">If the request succeeds:</span></span>

* <span data-ttu-id="dc942-185">201 (만들어짐) 응답을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-185">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="dc942-186">응답의 Location 헤더의 생성된 된 리소스의 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-186">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="dc942-187">리소스를 업데이트 하는 PUT 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="dc942-187">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="dc942-188">다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-188">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="dc942-189">합니다 **PutAsJsonAsync** 메서드처럼 작동 **PostAsJsonAsync**POST 대신 PUT 요청을 전송 하는 점을 제외 하 고, 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-189">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="dc942-190">리소스를 삭제 하는 DELETE 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="dc942-190">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="dc942-191">다음 코드는 제품을 삭제 하는 DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-191">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="dc942-192">GET, 같은 삭제 요청 되지 않은 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-192">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="dc942-193">삭제를 사용 하 여 JSON 또는 XML 형식으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-193">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="dc942-194">샘플 테스트</span><span class="sxs-lookup"><span data-stu-id="dc942-194">Test the sample</span></span>

<span data-ttu-id="dc942-195">클라이언트 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-195">To test the client app:</span></span>

1. <span data-ttu-id="dc942-196">[다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 및 서버 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-196">[Download](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="dc942-197">[지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="dc942-197">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="dc942-198">서버 앱이 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-198">Verify the server app is working.</span></span> <span data-ttu-id="dc942-199">Exaxmple에 대 한 `http://localhost:64195/api/products` 제품 목록을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-199">For exaxmple, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="dc942-200">HTTP 요청에 대 한 기본 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-200">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="dc942-201">서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-201">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="dc942-202">클라이언트 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-202">Run the client app.</span></span> <span data-ttu-id="dc942-203">다음 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc942-203">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
