---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API의에서 협상 내용 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API HTTP 콘텐츠 협상을 구현 하는 방법에 대해 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/20/2012
ms.topic: article
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: ca373af6754e82889dc100b63f73b76aaa4e4f27
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26507022"
---
<a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="9d6bd-103">ASP.NET Web API의에서 콘텐츠 협상</span><span class="sxs-lookup"><span data-stu-id="9d6bd-103">Content Negotiation in ASP.NET Web API</span></span>
====================
<span data-ttu-id="9d6bd-104">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9d6bd-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9d6bd-105">이 문서에서는 ASP.NET Web API에서 콘텐츠 협상을 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-105">This article describes how ASP.NET Web API implements content negotiation.</span></span>

<span data-ttu-id="9d6bd-106">"여러 표현이 있는 경우 지정 된 응답에 대 한 가장 잘 표시를 선택 하는 프로세스입니다."와 콘텐츠 협상을 정의 하는 HTTP 사양 (RFC 2616)</span><span class="sxs-lookup"><span data-stu-id="9d6bd-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="9d6bd-107">Http에서 콘텐츠 협상에는 기본 메커니즘은 이러한 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="9d6bd-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="9d6bd-108">**수락:** 미디어 유형을 "application/json이"와 같은 응답에 대 한 허용 되는 "application/xml," 또는와 같은 사용자 지정 미디어 유형을 &quot;application/vnd.example+xml&quot;</span><span class="sxs-lookup"><span data-stu-id="9d6bd-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="9d6bd-109">**Accept-charset:** 는 문자 집합은 같은 utf-8 또는 ISO 8859-1입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="9d6bd-110">**허용 인코딩:** 콘텐츠 인코딩을 gzip과 같은 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="9d6bd-111">**수락 언어:** 기본 자연어와 같은 "en-us"입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="9d6bd-112">서버는 HTTP 요청의 다른 부분 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="9d6bd-113">예를 들어 X-요청한-와 헤더를 포함 하는 요청을 하는 경우 AJAX 요청을 나타내는 서버 기본적으로 JSON Accept 헤더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="9d6bd-114">이 문서에서는 웹 API 적용 및 Accept-charset 헤더를 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="9d6bd-115">(지금은 있습니다 Accept-encoding 또는 Accept-language에 대 한 기본 제공 지원이.)</span><span class="sxs-lookup"><span data-stu-id="9d6bd-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="9d6bd-116">Serialization</span><span class="sxs-lookup"><span data-stu-id="9d6bd-116">Serialization</span></span>

<span data-ttu-id="9d6bd-117">CLR 형식으로 리소스를 반환 하는 Web API 컨트롤러, 파이프라인 반환 값 또는 그 반대로 serialize 하 고 HTTP 응답 본문에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="9d6bd-118">예를 들어 컨트롤러 동작:</span><span class="sxs-lookup"><span data-stu-id="9d6bd-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="9d6bd-119">클라이언트가이 HTTP 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="9d6bd-120">에 대 한 응답 서버 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="9d6bd-121">이 예제에서는 클라이언트 요청 JSON, Javascript, 또는 "항목" (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="9d6bd-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="9d6bd-122">응답의 JSON 표현으로 받은 서버는 `Product` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-122">The server responsed with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="9d6bd-123">응답에서 Content-type 헤더가로 설정 되는 &quot;응용 프로그램/json&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="9d6bd-124">컨트롤러를 반환할 수도 있습니다는 **HttpResponseMessage** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="9d6bd-125">응답 본문에 대 한 CLR 개체를 지정 하려면 호출는 **CreateResponse** 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="9d6bd-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="9d6bd-126">이 옵션에는 응답의 세부 사항에 대해 더 많은 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="9d6bd-127">상태 코드를 설정 하 고을 HTTP 헤더를 추가 하 고, 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="9d6bd-128">리소스를 직렬화 하는 개체 라고는 *미디어 포맷터*합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="9d6bd-129">미디어 포맷터가 파생 되는 **MediaTypeFormatter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="9d6bd-130">Web API 미디어 포맷터 XML 및 JSON을 하며 다른 미디어 형식을 지원 하기 위해 사용자 지정 포맷터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="9d6bd-131">사용자 지정 포맷터를 작성 하는 방법에 대 한 정보를 참조 하십시오. [미디어 포맷터](media-formatters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="9d6bd-132">콘텐츠 협상 작동</span><span class="sxs-lookup"><span data-stu-id="9d6bd-132">How Content Negotiation Works</span></span>

<span data-ttu-id="9d6bd-133">첫째, 파이프라인 가져옵니다는 **IContentNegotiator** 서비스는 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="9d6bd-134">또한 미디어 포맷터에서의 목록을 가져옵니다는 **HttpConfiguration.Formatters** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="9d6bd-135">그런 다음 파이프라인 호출 **IContentNegotiatior.Negotiate**을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-135">Next, the pipeline calls **IContentNegotiatior.Negotiate**, passing in:</span></span>

- <span data-ttu-id="9d6bd-136">직렬화 할 개체의 유형</span><span class="sxs-lookup"><span data-stu-id="9d6bd-136">The type of object to serialize</span></span>
- <span data-ttu-id="9d6bd-137">미디어 포맷터의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="9d6bd-137">The collection of media formatters</span></span>
- <span data-ttu-id="9d6bd-138">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9d6bd-138">The HTTP request</span></span>

<span data-ttu-id="9d6bd-139">**Negotiate** 메서드는 두 가지 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="9d6bd-140">사용 하는 포맷터</span><span class="sxs-lookup"><span data-stu-id="9d6bd-140">Which formatter to use</span></span>
- <span data-ttu-id="9d6bd-141">응답에 대 한 미디어 유형</span><span class="sxs-lookup"><span data-stu-id="9d6bd-141">The media type for the response</span></span>

<span data-ttu-id="9d6bd-142">포맷터가 있으면는 **Negotiate** 메서드 반환 **null**, 클라이언트 받는 HTTP 오류 406 (승인 금지).</span><span class="sxs-lookup"><span data-stu-id="9d6bd-142">If no formatter is found, the **Negotiate** method returns **null**, and the client recevies HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="9d6bd-143">다음 코드는 컨트롤러 콘텐츠 협상 수 직접 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="9d6bd-144">이 코드는 해당 하는 파이프라인에서 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="9d6bd-145">기본 콘텐츠 협상 자입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-145">Default Content Negotiator</span></span>

<span data-ttu-id="9d6bd-146">**DefaultContentNegotiator** 클래스의 기본 구현을 제공 **IContentNegotiator**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="9d6bd-147">다양 한 조건을 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="9d6bd-148">첫째, 포맷터 형식을 직렬화 할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="9d6bd-149">이 호출 하 여 확인 됩니다 **MediaTypeFormatter.CanWriteType**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="9d6bd-150">다음으로 콘텐츠 협상 자 각 포맷터에 얼마나 잘 HTTP 요청을 일치를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="9d6bd-151">일치 하는 평가 하 고, 콘텐츠 협상 자 기능에서는 다음 두 가지 포맷터에:</span><span class="sxs-lookup"><span data-stu-id="9d6bd-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="9d6bd-152">**SupportedMediaTypes** 지원 되는 미디어 형식 목록이 포함 된 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="9d6bd-153">콘텐츠 협상 자 요청 Accept 헤더에 대해이 목록에 일치 시 키 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="9d6bd-154">참고 Accept 헤더가 범위를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="9d6bd-155">예를 들어 "텍스트/plain"은 텍스트와 일치 하는 /\* 또는 \* / \*합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="9d6bd-156">**MediaTypeMappings** 목록을 포함 하는 컬렉션 **MediaTypeMapping** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="9d6bd-157">**MediaTypeMapping** 클래스는 HTTP 요청을 미디어 형식과 일치 하는 일반적인 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="9d6bd-158">예를 들어 특정 미디어 유형에 사용자 지정 HTTP 헤더를 매핑할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="9d6bd-159">여러 개의 일치, 최고 품질 비율 wins와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="9d6bd-160">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="9d6bd-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="9d6bd-161">이 예제에서는 응용 프로그램/json에 응용 프로그램/xml을 통해 기본 있으므로 1.0은 암시적된 품질 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="9d6bd-162">일치 하는 경우 콘텐츠 협상 자 다시 일치 하는 요청 본문의 미디어 형식에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="9d6bd-163">예를 들어, JSON 데이터를 포함 하는 요청을 콘텐츠 협상 자 JSON 포맷터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="9d6bd-164">남아 있는 경우 일치 하는 항목, 콘텐츠 협상 자는 단순히 형식을 serialize 할 수 있는 첫 번째 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="9d6bd-165">문자 인코딩을 선택</span><span class="sxs-lookup"><span data-stu-id="9d6bd-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="9d6bd-166">콘텐츠 협상 자 최상의 문자 인코딩을 확인 하 여 선택 하는 포맷터를 선택한 후는 **SupportedEncodings** 포맷터 및 (있는 경우) 요청에 Accept-charset 헤더에 대해 검색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6bd-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
