---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2의에서 미디어 포맷터 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: 1cb1c7e0f832a0a0160276fbd41facc017e2ae3e
ms.sourcegitcommit: 50d40c83fa641d283c097f986dde5341ebe1b44c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
---
<a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="86e90-102">ASP.NET Web API 2의에서 미디어 포맷터</span><span class="sxs-lookup"><span data-stu-id="86e90-102">Media Formatters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="86e90-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="86e90-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="86e90-104">이 자습서에는 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-104">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="86e90-105">인터넷 미디어 유형</span><span class="sxs-lookup"><span data-stu-id="86e90-105">Internet Media Types</span></span>

<span data-ttu-id="86e90-106">데이터의 형식을 식별 하는 MIME 형식이 라고도 하는 미디어 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-106">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="86e90-107">HTTP, 미디어 유형에 대해 메시지 본문의 형식은 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-107">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="86e90-108">미디어 유형은 두 문자열, 형식 및 하위 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-108">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="86e90-109">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="86e90-109">For example:</span></span>

- <span data-ttu-id="86e90-110">html 텍스트 /</span><span class="sxs-lookup"><span data-stu-id="86e90-110">text/html</span></span>
- <span data-ttu-id="86e90-111">이미지/png</span><span class="sxs-lookup"><span data-stu-id="86e90-111">image/png</span></span>
- <span data-ttu-id="86e90-112">application/json</span><span class="sxs-lookup"><span data-stu-id="86e90-112">application/json</span></span>

<span data-ttu-id="86e90-113">HTTP 메시지에 엔터티 본문이 포함 되어 있으면, 콘텐츠 형식 헤더는 메시지 본문의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-113">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="86e90-114">이렇게 하면 수신자는 메시지 본문의 내용을 구문 분석 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-114">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="86e90-115">예를 들어 PNG 이미지를 포함 하는 HTTP 응답을 응답에 다음 헤더 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-115">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="86e90-116">클라이언트 요청 메시지를 보내면 Accept 헤더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-116">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="86e90-117">Accept 헤더는 미디어 유형의 클라이언트 서버는 서버에서 원하는 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-117">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="86e90-118">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="86e90-118">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="86e90-119">이 헤더 클라이언트가 HTML, XHTML 또는 XML을 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-119">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="86e90-120">미디어 유형 웹 API를 직렬화 및 역직렬화 HTTP 메시지 본문 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-120">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="86e90-121">Web API에서 기본적으로 XML, JSON, BSON, 및 양식 인코딩된 데이터를 지원 하 고 작성 하 여 추가 미디어 유형을 지원할 수 있습니다는 *미디어 포맷터*합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-121">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="86e90-122">미디어 포맷터를 만들려면 이러한 클래스 중 하나에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-122">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="86e90-123">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e90-123">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="86e90-124">이 클래스는 비동기 읽기 및 쓰기 메서드.</span><span class="sxs-lookup"><span data-stu-id="86e90-124">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="86e90-125">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e90-125">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="86e90-126">이 클래스에서 파생 **MediaTypeFormatter** 하지만 sychronous 읽기/쓰기 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-126">This class derives from **MediaTypeFormatter** but uses sychronous read/write methods.</span></span>

<span data-ttu-id="86e90-127">파생 된 **BufferedMediaTypeFormatter** 은 코드가 없는 비동기 I/O 중 호출 스레드를 차단할 수 의미 하기 때문에 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-127">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="86e90-128">예: CSV 미디어 포맷터 생성</span><span class="sxs-lookup"><span data-stu-id="86e90-128">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="86e90-129">다음 예제를 쉼표로 구분 된 값 (CSV) 형식에서 제품 개체를 serialize 할 수 있는 미디어 유형 포맷터를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-129">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="86e90-130">이 예제에서는 자습서에 정의 된 제품 유형을 사용 하 여 [CRUD 작업을 지원 합니다. 해당 웹 API를 만드는](../older-versions/creating-a-web-api-that-supports-crud-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-130">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="86e90-131">제품 개체의 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-131">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="86e90-132">파생 되는 클래스 정의 CSV 포맷터를 구현 하려면 **BufferedMediaTypeFormater**:</span><span class="sxs-lookup"><span data-stu-id="86e90-132">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormater**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="86e90-133">생성자에 포맷터가 지 원하는 미디어 유형에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-133">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="86e90-134">포맷터가 단일 미디어 형식을 지 원하는이 예제에서는 &quot;텍스트/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="86e90-134">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="86e90-135">재정의 **CanWriteType** 포맷터 유형을 나타내도록 메서드를 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-135">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="86e90-136">이 예제에서는 포맷터를 serialize 할 수 단일 `Product` 개체의 컬렉션 뿐만 아니라 `Product` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-136">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="86e90-137">마찬가지로, 재정의 **CanReadType** 포맷터 유형을 나타내도록 메서드를 역직렬화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-137">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="86e90-138">이 예제에서는 포맷터 지원 하지 않습니다 deserialization 메서드는 단순히 반환 하므로 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-138">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="86e90-139">마지막으로, 재정의 **WriteToStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="86e90-139">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="86e90-140">이 메서드는 스트림에 작성 하 여 형식을 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-140">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="86e90-141">포맷터가 deserialization을 지 원하는 경우 재정의 **ReadFromStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="86e90-141">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="86e90-142">Web API 파이프라인에 미디어 포맷터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-142">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="86e90-143">미디어 유형 포맷터를 Web API 파이프라인을 추가 하려면 사용 된 **포맷터** 속성에는 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-143">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="86e90-144">문자 인코딩</span><span class="sxs-lookup"><span data-stu-id="86e90-144">Character Encodings</span></span>

<span data-ttu-id="86e90-145">필요에 따라 미디어 포맷터는 ISO 8859-1 또는 u t F-8와 같은 여러 문자 인코딩을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-145">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="86e90-146">생성자를 하나 이상 추가 [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) 형식을 **SupportedEncodings** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-146">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="86e90-147">기본을 인코딩 첫 번째 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-147">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="86e90-148">에 **WriteToStream** 및 **ReadFromStream** 메서드를 호출 [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) 기본 문자 인코딩을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-148">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="86e90-149">이 메서드는 지원 되는 인코딩 목록에 대해 요청 헤더와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="86e90-149">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="86e90-150">사용 하 여 반환 된 **인코딩** 읽거나 쓸 스트림의:</span><span class="sxs-lookup"><span data-stu-id="86e90-150">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
