---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: "ASP.NET Web API 2.1의에서 BSON 지원 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 53ad705fad6d2225cecca4d73355bd6ebfcf56d5
ms.sourcegitcommit: 459cb3289741a3f46325e605a617dc926ee0563d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
<a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="c6def-102">ASP.NET Web API 2.1의에서 BSON 지원</span><span class="sxs-lookup"><span data-stu-id="c6def-102">BSON Support in ASP.NET Web API 2.1</span></span>
====================
<span data-ttu-id="c6def-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c6def-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c6def-104">Web API 2.1에서는 BSON 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-104">Web API 2.1 introduces support for BSON.</span></span> <span data-ttu-id="c6def-105">이 항목에서는 Web API 컨트롤러 (서버 쪽) 및.NET 클라이언트 앱 BSON을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span>

## <a name="what-is-bson"></a><span data-ttu-id="c6def-106">BSON 란?</span><span class="sxs-lookup"><span data-stu-id="c6def-106">What is BSON?</span></span>

<span data-ttu-id="c6def-107">[BSON](http://bsonspec.org/) 은 이진 serialization 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-107">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="c6def-108">"BSON"은 "Binary JSON" 있지만 BSON 및 JSON 매우 다르게 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-108">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="c6def-109">BSON은 "JSON 유사한" 이므로 개체를 JSON 비슷한 이름-값 쌍으로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-109">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="c6def-110">JSON, 달리 숫자 데이터 형식이 문자열이 아니라를 바이트로 저장</span><span class="sxs-lookup"><span data-stu-id="c6def-110">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="c6def-111">BSON 가볍고, 스캔 하기 쉬운 인코딩/디코딩에 빠른 되도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-111">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="c6def-112">BSON는 JSON 크기가 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-112">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="c6def-113">데이터에 따라 BSON 페이로드 JSON 페이로드 보다 크거나 작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-113">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="c6def-114">이미지 파일과 같은 이진 데이터를 직렬화 하는 작업에 대 한 없기 때문에 이진 데이터가 base64 인코딩 BSON는 JSON, 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-114">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="c6def-115">BSON 문서는 쉽게 요소 라는 접두사가 길이 필드 이므로 파서에서 디코딩하지 않고도 요소를 건너뛸 수 때문에 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-115">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="c6def-116">인코딩 및 디코딩하는 숫자 데이터 형식이 문자열이 아니라 숫자로 저장 되기 때문에, 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-116">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="c6def-117">.NET 클라이언트 앱 등의 네이티브 클라이언트 BSON JSON 또는 XML과 같은 텍스트 기반 형식 대신 사용 하 여 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-117">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="c6def-118">브라우저 클라이언트에 대 한 싶을 것 환경에 JSON, JavaScript JSON 페이로드를 직접 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-118">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="c6def-119">웹 API에 사용 다행히 [콘텐츠 협상](content-negotiation.md)하므로 API에서 두 가지 형식 모두를 지원 하 고 선택 하면 클라이언트 수, 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-119">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="c6def-120">BSON 서버에서 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c6def-120">Enabling BSON on the Server</span></span>

<span data-ttu-id="c6def-121">Web API 구성에 추가 **BsonMediaTypeFormatter** 포맷터 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-121">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="c6def-122">이제는 클라이언트가 "응용 프로그램/bson"를 요청 하는 경우 웹 API BSON 포맷터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-122">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="c6def-123">BSON 다른 미디어 유형에 연결할 SupportedMediaTypes 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-123">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="c6def-124">다음 코드는 지원 되는 미디어 형식에 "application/vnd.contoso"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-124">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="c6def-125">HTTP 세션 예제</span><span class="sxs-lookup"><span data-stu-id="c6def-125">Example HTTP Session</span></span>

<span data-ttu-id="c6def-126">이 예에서는 간단한 Web API 컨트롤러 및 다음과 같은 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-126">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="c6def-127">클라이언트는 다음 HTTP 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-127">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="c6def-128">다음은 응답이입니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-128">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="c6def-129">여기에서 이진 데이터를 바꾸어도 &quot;.&quot; 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-129">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="c6def-130">다음 스크린 샷에서 원시 16 진수 값에서 Fiddler 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-130">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="c6def-131">BSON HttpClient 사용</span><span class="sxs-lookup"><span data-stu-id="c6def-131">Using BSON with HttpClient</span></span>

<span data-ttu-id="c6def-132">.NET 클라이언트 앱 BSON 포맷터를 사용할 수 있습니다 **HttpClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-132">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="c6def-133">에 대 한 자세한 내용은 **HttpClient**, 참조 [웹 API에서 정도.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-133">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="c6def-134">다음 코드는 BSON을 받아들이고 다음 응답에 BSON 페이로드를 역직렬화 하는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-134">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="c6def-135">BSON을 서버에서 요청 하려면 Accept 헤더 "응용 프로그램/bson"를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-135">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="c6def-136">응답 본문을 deserialize 하는 데 사용 된 **BsonMediaTypeFormatter**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-136">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="c6def-137">이 포맷터 하지 않으므로 기본 포맷터 컬렉션에서 응답 본문을 읽을 때 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-137">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="c6def-138">다음 예제에서는 BSON 포함 된 POST 요청을 전송 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-138">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="c6def-139">이 코드의 대부분은 앞의 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-139">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="c6def-140">하지만 **PostAsync** 메서드를 지정 **BsonMediaTypeFormatter** 포맷터로:</span><span class="sxs-lookup"><span data-stu-id="c6def-140">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="c6def-141">최상위 기본 형식 직렬화</span><span class="sxs-lookup"><span data-stu-id="c6def-141">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="c6def-142">모든 BSON 문서는 키/값 쌍의 목록입니다. BSON 사양에는 정수 또는 문자열과 같은 단일 원시 값을 직렬화 하는 작업에 대 한 구문을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-142">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="c6def-143">이 제한을 해결 하는 **BsonMediaTypeFormatter** 특별 한 경우 기본 형식 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-143">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="c6def-144">직렬화 하는 작업을 하기 전에 변환 값 키/값 쌍으로 "Value" 키를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-144">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="c6def-145">예를 들어 정수를 반환 하는 API 컨트롤러 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-145">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="c6def-146">직렬화 하는 작업을 하기 전에 BSON 포맷터 키/값 쌍에 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-146">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="c6def-147">Deserialize 하면 포맷터 원래 값으로 다시 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-147">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="c6def-148">그러나 다른 BSON 파서를 사용 하 여 클라이언트는 web API 원시 값을 반환 하는 경우이 경우를 처리 하 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-148">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="c6def-149">일반적으로 원시 값 보다는 구조화 된 데이터를 반환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6def-149">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6def-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c6def-150">Additional Resources</span></span>

[<span data-ttu-id="c6def-151">웹 API BSON 샘플</span><span class="sxs-lookup"><span data-stu-id="c6def-151">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="c6def-152">미디어 포맷터</span><span class="sxs-lookup"><span data-stu-id="c6def-152">Media Formatters</span></span>](media-formatters.md)
