---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: "JSON 및 ASP.NET Web API의에서 XML Serialization | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2012
ms.topic: article
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 7aafe4823d3a6090fae4a63f1a66fb2670ecb025
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="8f6ca-102">JSON 및 ASP.NET Web API의에서 XML 직렬화</span><span class="sxs-lookup"><span data-stu-id="8f6ca-102">JSON and XML Serialization in ASP.NET Web API</span></span>
====================
<span data-ttu-id="8f6ca-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8f6ca-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8f6ca-104">이 문서에서는 ASP.NET Web API의 JSON과 XML 포맷터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-104">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="8f6ca-105">ASP.NET Web API에는 *미디어 유형 포맷터* 는 개체 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-105">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="8f6ca-106">HTTP에서 읽기 CLR 개체로 메시지 본문</span><span class="sxs-lookup"><span data-stu-id="8f6ca-106">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="8f6ca-107">CLR 개체는 HTTP 메시지 본문에 쓰기</span><span class="sxs-lookup"><span data-stu-id="8f6ca-107">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="8f6ca-108">Web API는 JSON 및 XML에 대 한 미디어 유형 포맷터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-108">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="8f6ca-109">프레임 워크는 기본적으로 파이프라인에 이러한 포맷터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-109">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="8f6ca-110">클라이언트는 HTTP 요청의 Accept 헤더에서 JSON 또는 XML 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-110">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="8f6ca-111">목차</span><span class="sxs-lookup"><span data-stu-id="8f6ca-111">Contents</span></span>

- [<span data-ttu-id="8f6ca-112">JSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-112">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="8f6ca-113">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="8f6ca-113">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="8f6ca-114">날짜</span><span class="sxs-lookup"><span data-stu-id="8f6ca-114">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="8f6ca-115">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="8f6ca-115">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="8f6ca-116">카멜식 대/소문자</span><span class="sxs-lookup"><span data-stu-id="8f6ca-116">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="8f6ca-117">익명 및 약한 형식의 개체</span><span class="sxs-lookup"><span data-stu-id="8f6ca-117">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="8f6ca-118">XML 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-118">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="8f6ca-119">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="8f6ca-119">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="8f6ca-120">날짜</span><span class="sxs-lookup"><span data-stu-id="8f6ca-120">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="8f6ca-121">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="8f6ca-121">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="8f6ca-122">형식당 하나의 XML 직렬 변환기 설정</span><span class="sxs-lookup"><span data-stu-id="8f6ca-122">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="8f6ca-123">JSON 또는 XML 포맷터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-123">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="8f6ca-124">순환 개체 참조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-124">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="8f6ca-125">테스트 개체 Serialization</span><span class="sxs-lookup"><span data-stu-id="8f6ca-125">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="8f6ca-126">JSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-126">JSON Media-Type Formatter</span></span>

<span data-ttu-id="8f6ca-127">JSON 형식 지정에서 제공 되는 **JsonMediaTypeFormatter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-127">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="8f6ca-128">기본적으로 **JsonMediaTypeFormatter** 사용 하 여는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 직렬화를 수행 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-128">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="8f6ca-129">Json.NET 타사 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-129">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="8f6ca-130">원하는 경우 구성할 수 있습니다는 **JsonMediaTypeFormatter** 사용 하는 클래스는 **DataContractJsonSerializer** Json.NET 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-130">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="8f6ca-131">이 위해 설정 된 **UseDataContractJsonSerializer** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-131">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="8f6ca-132">JSON serialization</span><span class="sxs-lookup"><span data-stu-id="8f6ca-132">JSON Serialization</span></span>

<span data-ttu-id="8f6ca-133">이 섹션에서는 기본값을 사용 하 여 JSON 포맷터의 몇 가지 특정 동작을 설명 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-133">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="8f6ca-134">Json.NET library;의 광범위 한 문서 수를 다루지는지 않습니다. 자세한 내용은 참조는 [Json.NET 설명서](http://james.newtonking.com/projects/json/help/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-134">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="8f6ca-135">Serialize 되는 요소?</span><span class="sxs-lookup"><span data-stu-id="8f6ca-135">What Gets Serialized?</span></span>

<span data-ttu-id="8f6ca-136">기본적으로 모든 public 속성과 필드가 serialize 된 JSON에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-136">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="8f6ca-137">속성 또는 필드를 생략 하려면으로 데코레이팅는 **JsonIgnore** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-137">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="8f6ca-138">원하는 경우는 &quot;옵트인&quot; 접근을 사용 하 여 클래스를 데코레이팅하는 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-138">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="8f6ca-139">이 특성이 있는 경우 멤버를가지고 무시 하 고 **DataMember**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-139">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="8f6ca-140">사용할 수도 있습니다 **DataMember** 전용 멤버를 serialize 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-140">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="8f6ca-141">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="8f6ca-141">Read-Only Properties</span></span>

<span data-ttu-id="8f6ca-142">읽기 전용 속성은 기본적으로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-142">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="8f6ca-143">날짜</span><span class="sxs-lookup"><span data-stu-id="8f6ca-143">Dates</span></span>

<span data-ttu-id="8f6ca-144">날짜에 Json.NET 기본적으로 기록 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-144">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="8f6ca-145">Utc (협정 세계시) 날짜 "Z" 접미사와 함께 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-145">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="8f6ca-146">현지 시간에서 날짜는 표준 시간대 오프셋을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-146">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="8f6ca-147">예:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-147">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="8f6ca-148">기본적으로 Json.NET 표준 시간대를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-148">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="8f6ca-149">DateTimeZoneHandling 속성을 설정 하 여이 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-149">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="8f6ca-150">사용 하려는 경우 [Microsoft JSON 날짜 형식](https://msdn.microsoft.com/en-us/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) ISO 8601 대신 설정는 **DateFormatHandling** serializer 설정에는 속성:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-150">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/en-us/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="8f6ca-151">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="8f6ca-151">Indenting</span></span>

<span data-ttu-id="8f6ca-152">들여쓰기 된 JSON을 작성 하기 위해 설정 된 **서식** 설정을 **Formatting.Indented**:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-152">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="8f6ca-153">카멜식 대/소문자</span><span class="sxs-lookup"><span data-stu-id="8f6ca-153">Camel Casing</span></span>

<span data-ttu-id="8f6ca-154">데이터 모델을 변경 하지 않고 JSON 속성 이름은 카멜식 대/소문자를 작성 하려면 설정는 **CamelCasePropertyNamesContractResolver** serializer에:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-154">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="8f6ca-155">익명 및 약한 형식의 개체</span><span class="sxs-lookup"><span data-stu-id="8f6ca-155">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="8f6ca-156">동작 메서드 익명 개체 되돌린 JSON으로 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-156">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="8f6ca-157">예:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-157">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="8f6ca-158">응답 메시지 본문에는 다음 JSON 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-158">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="8f6ca-159">위해 요청 본문을 deserialize 할 수 있는 웹 API 느슨하게 수신 구성 하 고 클라이언트에서 JSON 개체, 하는 경우는 **Newtonsoft.Json.Linq.JObject** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-159">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="8f6ca-160">그러나 강력한 형식의 데이터 개체를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-160">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="8f6ca-161">그런 다음, 직접 데이터를 구문 분석 필요가 없습니다 및 모델 유효성 검사의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-161">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="8f6ca-162">XML serializer 익명 형식을 지원 하지 않습니다 또는 **JObject** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-162">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="8f6ca-163">JSON 데이터에 대 한 이러한 기능을 사용 하는 경우이 문서의 뒷부분에 설명 된 대로 파이프라인에서 XML 포맷터를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-163">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="8f6ca-164">XML 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-164">XML Media-Type Formatter</span></span>

<span data-ttu-id="8f6ca-165">XML 서식 지정에서 제공 되는 **XmlMediaTypeFormatter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-165">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="8f6ca-166">기본적으로 **XmlMediaTypeFormatter** 사용 하 여는 **DataContractSerializer** 클래스를 직렬화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-166">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="8f6ca-167">원하는 경우 구성할 수 있습니다는 **XmlMediaTypeFormatter** 사용 하 여 **XmlSerializer** 대신는 **DataContractSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-167">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="8f6ca-168">이 위해 설정 된 **UseXmlSerializer** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-168">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="8f6ca-169">**XmlSerializer** 클래스 형식 보다 적은 집합 지원 **DataContractSerializer**, 하지만 결과 XML에 대 한 더 많은 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-169">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="8f6ca-170">사용 하는 것이 좋습니다 **XmlSerializer** 기존 XML 스키마와 일치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-170">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="8f6ca-171">XML Serialization</span><span class="sxs-lookup"><span data-stu-id="8f6ca-171">XML Serialization</span></span>

<span data-ttu-id="8f6ca-172">이 섹션에서는 기본값을 사용 하 여 XML 포맷터의 몇 가지 특정 동작을 설명 **DataContractSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-172">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="8f6ca-173">기본적으로 DataContractSerializer는 다음과 같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-173">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="8f6ca-174">모든 공개 읽기/쓰기 속성과 필드가 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-174">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="8f6ca-175">속성 또는 필드를 생략 하려면으로 데코레이팅는 **IgnoreDataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-175">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="8f6ca-176">전용 및 보호 된 멤버를 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-176">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="8f6ca-177">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-177">Read-only properties are not serialized.</span></span> <span data-ttu-id="8f6ca-178">그러나 (읽기 전용 컬렉션 속성의 내용은 serialize 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="8f6ca-178">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="8f6ca-179">클래스 및 멤버 이름은 클래스 선언에 표시 된 대로 XML에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-179">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="8f6ca-180">기본 XML 네임 스페이스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-180">A default XML namespace is used.</span></span>

<span data-ttu-id="8f6ca-181">Serialization에 보다 자세히 제어 해야 할 경우 사용 하 여 클래스를 데코레이팅 할 수 있습니다는 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-181">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="8f6ca-182">이 특성이 있는 경우 클래스는 다음과 같이 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-182">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="8f6ca-183">&quot;옵트인&quot; 방법: 속성 및 필드는 기본적으로 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-183">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="8f6ca-184">속성 또는 필드를 직렬화 하는 데 사용 하 여를 데코레이팅하는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-184">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="8f6ca-185">Private 또는 protected 멤버를 serialize 하는 데 사용 하 여를 데코레이팅하는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-185">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="8f6ca-186">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-186">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="8f6ca-187">클래스 이름은 XML에 표시 되는 방식을 변경 하려면는 *이름* 에서 매개 변수는 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-187">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="8f6ca-188">멤버 이름은 XML에 표시 되는 방식을 변경 하려면는 *이름* 에서 매개 변수는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-188">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="8f6ca-189">XML 네임 스페이스를 변경 하려면 설정는 *Namespace* 에서 매개 변수는 **DataContract** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-189">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="8f6ca-190">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="8f6ca-190">Read-Only Properties</span></span>

<span data-ttu-id="8f6ca-191">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-191">Read-only properties are not serialized.</span></span> <span data-ttu-id="8f6ca-192">읽기 전용 속성에는 지원 전용 필드를 private 필드를 표시할 수 있습니다는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-192">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="8f6ca-193">이 접근 방식에서는 **DataContract** 클래스의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-193">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="8f6ca-194">날짜</span><span class="sxs-lookup"><span data-stu-id="8f6ca-194">Dates</span></span>

<span data-ttu-id="8f6ca-195">날짜는 ISO 8601 형식으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-195">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="8f6ca-196">예를 들어 &quot;2012-05-23T20:21:37.9116538Z&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-196">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="8f6ca-197">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="8f6ca-197">Indenting</span></span>

<span data-ttu-id="8f6ca-198">들여쓰기 한 XML를 작성 하려면 설정는 **들여쓰기** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-198">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="8f6ca-199">형식당 하나의 XML 직렬 변환기 설정</span><span class="sxs-lookup"><span data-stu-id="8f6ca-199">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="8f6ca-200">여러 CLR 유형에 다른 XML 직렬 변환기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-200">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="8f6ca-201">예를 들어 특정 데이터 개체에 필요한 해야할 **XmlSerializer** 이전 버전과 호환성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-201">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="8f6ca-202">사용할 수 있습니다 **XmlSerializer** 이 개체를 계속 사용 하려면 **DataContractSerializer** 다른 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-202">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="8f6ca-203">특정 형식에 대 한 XML serializer를 설정 하려면 호출 **SetSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-203">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="8f6ca-204">지정할 수는 **XmlSerializer** 또는 모든 개체에서 파생 된 **XmlObjectSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-204">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="8f6ca-205">JSON 또는 XML 포맷터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-205">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="8f6ca-206">사용 하지 않을 경우 포맷터 목록에서 JSON 포맷터 또는 XML 포맷터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-206">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="8f6ca-207">이 작업을 수행 하는 주된 이유는:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-207">The main reasons to do this are:</span></span>

- <span data-ttu-id="8f6ca-208">특정 미디어 유형의에 웹 API 응답을 제한 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-208">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="8f6ca-209">예를 들어만 JSON 응답을 지원 하 여 XML 포맷터를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-209">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="8f6ca-210">기본 포맷터를 사용자 지정 포맷터를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-210">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="8f6ca-211">예를 들어 JSON 포맷터 JSON 포맷터의 사용자 지정 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-211">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="8f6ca-212">다음 코드는 기본 포맷터를 제거 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-212">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="8f6ca-213">이 메서드를 호출 하면 **응용 프로그램\_시작** Global.asax에 정의 된 메서드.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-213">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="8f6ca-214">순환 개체 참조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-214">Handling Circular Object References</span></span>

<span data-ttu-id="8f6ca-215">기본적으로는 JSON과 XML 포맷터 값으로 모든 개체를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-215">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="8f6ca-216">두 속성이 같은 개체를 참조 하는 경우 또는 같은 개체 컬렉션에 두 번 표시 되 면 포맷터는 개체를 두 번 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-216">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="8f6ca-217">즉 특정 문제에 대 한 개체 그래프에는 주기를 포함 하는 경우 serializer는 그래프에는 루프를 감지 하는 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-217">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="8f6ca-218">다음과 같은 개체 모델 및 컨트롤러를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-218">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="8f6ca-219">이 작업을 호출 하면 포맷터를으로 변환 하는 상태 코드 500 (내부 서버 오류) 응답을 클라이언트에서 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-219">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="8f6ca-220">JSON에서 개체 참조를 유지 하려면 다음 코드를 추가 **응용 프로그램\_시작** Global.asax 파일에 대 한 메서드:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-220">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="8f6ca-221">이제 컨트롤러 작업에서는 다음과 같은 JSON을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-221">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="8f6ca-222">추가 하는 serializer는 &quot;$id&quot; 두 개체 모두에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-222">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="8f6ca-223">Employee.Department 속성 루프는 생성 값 개체 참조로 대체 하므로 검색 또한: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-223">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6ca-224">개체 참조는 표준 JSON에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-224">Object references are not standard in JSON.</span></span> <span data-ttu-id="8f6ca-225">이 기능을 사용 하기 전에 클라이언트 결과 구문 분석할 수 있는지 여부를 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-225">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="8f6ca-226">그래프에서 주기를 제거 하려면 단순히 좋을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-226">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="8f6ca-227">예를 들어,이 예제에서 직원 부서에 다시 링크 실제로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-227">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="8f6ca-228">XML에서 개체 참조를 유지 하려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-228">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="8f6ca-229">추가 하는 간단한 옵션은 `[DataContract(IsReference=true)]` 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-229">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="8f6ca-230">*IsReference* 개체 참조 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-230">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="8f6ca-231">에 유의 해야 **DataContract** 옵트인, serialization에서는 추가 해야 또한 있도록 **DataMember** 속성을 특성:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-231">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="8f6ca-232">포맷터와 유사한 XML 생성은 이제 다음과 같은:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-232">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="8f6ca-233">또 다른 옵션 모델 클래스에 특성을 방지 하려는 경우: 새 형식별 만들기 **DataContractSerializer** 인스턴스 및 설정 *preserveObjectReferences* 를 **true**  생성자에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-233">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="8f6ca-234">다음 XML 미디어 유형 포맷터의 형식당 하나의 serializer로이 인스턴스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-234">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="8f6ca-235">다음 코드에는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-235">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="8f6ca-236">테스트 개체 Serialization</span><span class="sxs-lookup"><span data-stu-id="8f6ca-236">Testing Object Serialization</span></span>

<span data-ttu-id="8f6ca-237">Web API를 디자인할 때에 데이터 개체를 serialize 하는 방법을 테스트 하려면 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-237">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="8f6ca-238">컨트롤러를 만들거나 컨트롤러 작업을 호출 하지 않고이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-238">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
