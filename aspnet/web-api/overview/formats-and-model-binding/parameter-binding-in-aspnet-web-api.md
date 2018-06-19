---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API의에서 바인딩 매개 변수 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2013
ms.topic: article
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5aa532137436922519c86246ebfa834910ac0d86
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042432"
---
<a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="b89f0-102">ASP.NET Web API의에서 바인딩 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b89f0-102">Parameter Binding in ASP.NET Web API</span></span>
====================
<span data-ttu-id="b89f0-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b89f0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b89f0-104">매개 변수를 호출 하는 프로세스에 대 한 값을 설정 해야 Web API 컨트롤러에서 메서드를 호출할 때 *바인딩*합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-104">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span> <span data-ttu-id="b89f0-105">이 문서에서는 웹 API 매개 변수를 바인딩하여 하는 방법에 대 한 바인딩 프로세스를 사용자 지정할 수는 어떻게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span>

<span data-ttu-id="b89f0-106">기본적으로 웹 API 매개 변수를 바인딩하는 다음 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-106">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="b89f0-107">매개 변수가 "simple" 형식인 경우 Web API URI에서 값을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-107">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="b89f0-108">단순 유형에.NET [기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, 등)를 더한 **TimeSpan**, **DateTime**, **Guid**, **10 진수**, 및 **문자열**, *플러스* 모든 문자열에서 변환할 수 있는 형식 변환기 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-108">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="b89f0-109">(에 대 한 자세한 나중에 형식 변환기입니다.)</span><span class="sxs-lookup"><span data-stu-id="b89f0-109">(More about type converters later.)</span></span>
- <span data-ttu-id="b89f0-110">사용 하 여 복합 형식의 경우 Web API 메시지 본문에서 값을 읽을 하려고에 대 한는 [미디어 유형 포맷터](media-formatters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-110">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="b89f0-111">예를 들어 다음은 일반적인 웹 API 컨트롤러 메서드에서가입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-111">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="b89f0-112">*id* 매개 변수는 한 &quot;간단한&quot; 입력, 웹 API 요청 URI에서에서 값을 가져오려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-112">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="b89f0-113">*항목* Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 값을 읽을 수 있도록 매개 변수는 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-113">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="b89f0-114">URI에서 값을 가져오려면 웹 API 경로 데이터 및 URI 쿼리 문자열에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-114">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="b89f0-115">경로 데이터 라우팅 시스템 URI 구문 분석 하는 경로에 일치 때 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-115">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="b89f0-116">자세한 내용은 참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-116">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="b89f0-117">이 문서의 나머지 부분에서는 모델 바인딩 프로세스를 사용자 지정할 수는 방법을 보여 드리 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-117">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="b89f0-118">그러나 복합 형식에 대 한 가능 하면 미디어 유형 포맷터를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b89f0-118">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="b89f0-119">HTTP의 핵심 원칙은 리소스가 있는 리소스의 표현을 지정 하려면 콘텐츠 협상을 사용 하 여 메시지 본문에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-119">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="b89f0-120">미디어 유형 포맷터는 정확 하 게이 목적을 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-120">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="b89f0-121">[FromUri]를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b89f0-121">Using [FromUri]</span></span>

<span data-ttu-id="b89f0-122">URI에서 복합 형식을 읽을 수 있는 웹 API를 강제로 표시 하려면 추가 **[FromUri]** 특성을 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-122">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="b89f0-123">다음 예제에서는 정의 `GeoPoint` 컨트롤러를 가져오는 메서드를 함께 종류는 `GeoPoint` URI에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-123">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="b89f0-124">클라이언트 쿼리 문자열의 위도 및 경도 값을 정렬할 수 및 Web API를 사용 하 여을 생성 한 `GeoPoint`합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-124">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="b89f0-125">예:</span><span class="sxs-lookup"><span data-stu-id="b89f0-125">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="b89f0-126">[FromBody]를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b89f0-126">Using [FromBody]</span></span>

<span data-ttu-id="b89f0-127">요청 본문에서 단순 형식을 읽을 수 있는 웹 API를 강제로 표시 하려면 추가 **[FromBody]** 특성을 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="b89f0-127">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="b89f0-128">이 예제에서는 웹 API를 사용 하 여 미디어 유형 포맷터의 값을 읽을 *이름* 요청 본문에서.</span><span class="sxs-lookup"><span data-stu-id="b89f0-128">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="b89f0-129">다음 예제에서는 클라이언트 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-129">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="b89f0-130">매개 변수는 [FromBody], 웹 API는 포맷터를 선택 하려면 콘텐츠 형식 헤더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-130">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="b89f0-131">이 예제에서는 콘텐츠 형식이 &quot;응용 프로그램/json&quot; 및 요청 본문은 원시 JSON 문자열 (JSON 개체).</span><span class="sxs-lookup"><span data-stu-id="b89f0-131">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="b89f0-132">최대 하나의 매개 변수는 메시지 본문에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-132">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="b89f0-133">따라서이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-133">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="b89f0-134">이 규칙에 대 한 이유는 요청 본문은 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림을에 보관할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-134">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="b89f0-135">형식 변환기</span><span class="sxs-lookup"><span data-stu-id="b89f0-135">Type Converters</span></span>

<span data-ttu-id="b89f0-136">만들어 (있도록 Web API는 URI에서에 연결 하려고) 클래스를 단순 형식으로 처리 하는 Web API를 만들 수 있습니다는 **TypeConverter** 문자열 변환을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-136">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="b89f0-137">다음 코드는 `GeoPoint` 지리적 시점을 나타내는 클래스 뒤에 **TypeConverter** 에서 문자열을 변환 하 `GeoPoint` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b89f0-137">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="b89f0-138">`GeoPoint` 로 데코레이팅된 클래스는 **[TypeConverter]** 형식 변환기를 지정 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-138">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="b89f0-139">(이 예에서는 Mike Stall 블로그 게시물에서 영감을 얻은 [작업 서명은 MVC/WebAPI에서의 사용자 지정 개체에 바인딩하는 방법을](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span><span class="sxs-lookup"><span data-stu-id="b89f0-139">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="b89f0-140">Web API에서 처리 하는 이제 `GeoPoint` 단순 형식으로 바인딩할 시도 것을 의미 `GeoPoint` URI에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-140">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="b89f0-141">포함할 필요가 없습니다 **[FromUri]** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-141">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="b89f0-142">클라이언트는 다음과 같은 URI 사용 하 여 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-142">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="b89f0-143">모델 바인더</span><span class="sxs-lookup"><span data-stu-id="b89f0-143">Model Binders</span></span>

<span data-ttu-id="b89f0-144">형식 변환기를 사용자 지정 모델 바인더를 만드는 것 보다 더 유연한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-144">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="b89f0-145">모델 바인더를 사용 하 여에서 액세스할 수 있는 등으로 HTTP 요청, 작업 설명 및 원시 값에 경로 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-145">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="b89f0-146">모델 바인더를 만들려면 구현는 **IModelBinder** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-146">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="b89f0-147">이 인터페이스는 단일 메서드를 정의 **BindModel**:</span><span class="sxs-lookup"><span data-stu-id="b89f0-147">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="b89f0-148">다음에 대 한 모델 바인더를은 `GeoPoint` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-148">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="b89f0-149">모델 바인더의 원시 입력된 값을 가져옵니다는 *값 공급자*합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-149">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="b89f0-150">이 설계에서는 두 가지 고유 함수를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-150">This design separates two distinct functions:</span></span>

- <span data-ttu-id="b89f0-151">값 공급자는 HTTP 요청을 사용 하 고 키-값 쌍의 사전을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-151">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="b89f0-152">모델 바인더가이 사전을 사용 하 여 모델을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-152">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="b89f0-153">Web API의 기본 값 공급자에서 경로 데이터 및 쿼리 문자열 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-153">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="b89f0-154">예를 들어, URI가 `http://localhost/api/values/1?location=48,-122`, 값 공급자는 다음 키-값 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-154">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="b89f0-155">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="b89f0-155">id = &quot;1&quot;</span></span>
- <span data-ttu-id="b89f0-156">위치 = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="b89f0-156">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="b89f0-157">(않는 기본 경로 템플릿을 한다고 가정 &quot;api / {controller} / {id}&quot;.)</span><span class="sxs-lookup"><span data-stu-id="b89f0-157">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="b89f0-158">바인딩할 매개 변수 이름에 저장 됩니다는 **ModelBindingContext.ModelName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-158">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="b89f0-159">모델 바인더 사전에이 값을 사용 하 여 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-159">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="b89f0-160">값으로 변환 될 수 있고 한 `GeoPoint`, 모델 바인더에 바인딩된 값을 할당는 **ModelBindingContext.Model** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-160">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="b89f0-161">공지 모델 바인더는 단순 형식 변환을 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-161">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="b89f0-162">이 예제에서는 모델 바인더 알려진된 위치의 테이블에서 먼저 찾습니다 및 형식 변환을 사용 하 여 실패할 경우.</span><span class="sxs-lookup"><span data-stu-id="b89f0-162">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="b89f0-163">**모델 바인더를 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="b89f0-163">**Setting the Model Binder**</span></span>

<span data-ttu-id="b89f0-164">모델 바인더를 설정 하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-164">There are several ways to set a model binder.</span></span> <span data-ttu-id="b89f0-165">첫째, 추가할 수 있습니다는 **[ModelBinder]** 특성을 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-165">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="b89f0-166">추가할 수도 있습니다는 **[ModelBinder]** 특성을 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-166">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="b89f0-167">Web API는 해당 형식의 모든 매개 변수에 대해 지정 된 모델 바인더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-167">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="b89f0-168">마지막으로, 모델 바인더 공급자를 추가할 수 있습니다는 **HttpConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-168">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="b89f0-169">모델 바인더 공급자는 모델 바인더를 만드는 팩터리 클래스 단순히 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-169">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="b89f0-170">파생 하 여 공급자를 만들 수는 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-170">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="b89f0-171">그러나 단일 형식을 처리 하는 모델 바인더를 경우 기본 제공 사용 하기 쉽게 **SimpleModelBinderProvider**,이 목적을 위해 디자인 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-171">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="b89f0-172">다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-172">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="b89f0-173">모델 바인딩 공급자와도 추가 해야는 **[ModelBinder]** 특성을 모델 바인더 및 미디어 유형 포맷터 하지 사용 해야 함을 웹 API를 구별 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-173">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="b89f0-174">하지만 이제 특성에 모델 바인더의 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-174">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="b89f0-175">값 공급자</span><span class="sxs-lookup"><span data-stu-id="b89f0-175">Value Providers</span></span>

<span data-ttu-id="b89f0-176">언급 한 모델 바인더 값 공급자에서 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-176">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="b89f0-177">사용자 지정 값 공급자를 작성 하려면 구현 된 **IValueProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-177">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="b89f0-178">요청에서 쿠키의 값을 가져오는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-178">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="b89f0-179">파생 하 여 값 공급자 팩터리를 만들 필요가 **ValueProviderFactory** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-179">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="b89f0-180">값 공급자 팩터리를 추가 **HttpConfiguration** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-180">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="b89f0-181">Web API 하므로 모든 값 공급자 작성 한 모델 바인더를 호출 하는 경우 **ValueProvider.GetValue**, 모델 바인더를 만들 수 있는 첫 번째 값 공급자에서 값을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-181">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="b89f0-182">사용 하 여 매개 변수 수준에서 값 공급자 팩터리를 설정할 수는 또한는 **ValueProvider** 특성을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-182">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="b89f0-183">지정 된 값 공급자 팩터리 모델 바인딩을 사용 하 고 사용 하지 않는 다른 등록 된 값 공급자의 웹 API 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-183">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="b89f0-184">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="b89f0-184">HttpParameterBinding</span></span>

<span data-ttu-id="b89f0-185">모델 바인더는 보다 일반적인 메커니즘의 특정 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-185">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="b89f0-186">보면는 **[ModelBinder]** 특성 나타납니다 추상에서 파생 되며 **ParameterBindingAttribute** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-186">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="b89f0-187">이 클래스는 단일 메서드를 정의 **GetBinding**를 반환 하는 **HttpParameterBinding** 개체:</span><span class="sxs-lookup"><span data-stu-id="b89f0-187">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="b89f0-188">**HttpParameterBinding** 매개 변수 값에 바인딩할 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-188">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="b89f0-189">경우 **[ModelBinder]**, 특성을 반환는 **HttpParameterBinding** 구현을 사용 하는 **IModelBinder** 실제 바인딩을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-189">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="b89f0-190">구현할 수도 있습니다 직접 **HttpParameterBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-190">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="b89f0-191">예를 들어, Etag에서 가져오려는 `if-match` 및 `if-none-match` 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-191">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="b89f0-192">Etag를 나타내는 클래스를 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-192">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="b89f0-193">ETag를 가져올 것인지를 지정 하는 열거형 정의 `if-match` 헤더 또는 `if-none-match` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-193">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="b89f0-194">다음은 **HttpParameterBinding** 하는 ETag에서 원하는 헤더 가져오고 ETag 형식의 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-194">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="b89f0-195">**ExecuteBindingAsync** 메서드는 바인딩을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-195">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="b89f0-196">이 메서드 내에서 추가 바인딩된 매개 변수 값은 **ActionArgument** 사전에는 **HttpActionContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-196">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="b89f0-197">경우에 **ExecuteBindingAsync** 메서드 요청 메시지의 본문을 읽고, 재정의 **WillReadBody** 속성을 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-197">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="b89f0-198">요청 본문은 한 버퍼링 되지 않은 스트림을 읽을 수만 있고 한 번, 웹 API 적용 규칙 최대 하나의 바인딩 메시지 본문을 읽을 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-198">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>


<span data-ttu-id="b89f0-199">사용자 지정을 적용 하려면 **HttpParameterBinding**에서 파생 되는 특성을 정의할 수 있습니다 **ParameterBindingAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-199">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="b89f0-200">에 대 한 `ETagParameterBinding`에 대 한 두 가지 특성을 정의 하겠습니다 `if-match` 머리글과 대 한 `if-none-match` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-200">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="b89f0-201">둘 다 추상 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-201">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="b89f0-202">다음은 사용 하는 컨트롤러 메서드는 `[IfNoneMatch]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-202">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="b89f0-203">외에 **ParameterBindingAttribute**, 사용자 지정을 추가 하기 위한 다른 후크는 **HttpParameterBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-203">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="b89f0-204">에 **HttpConfiguration** 개체는 **ParameterBindingRules** 속성은 형식의 anomymous 함수의 컬렉션 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**).</span><span class="sxs-lookup"><span data-stu-id="b89f0-204">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anomymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="b89f0-205">예를 들어 GET 메서드의 모든 ETag 매개 변수를 사용 하는 규칙을 추가할 수 있습니다 `ETagParameterBinding` 와 `if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="b89f0-205">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="b89f0-206">함수 반환 해야 `null` 바인딩을 적용할 수 없는 매개 변수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-206">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="b89f0-207">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="b89f0-207">IActionValueBinder</span></span>

<span data-ttu-id="b89f0-208">전체 매개 변수 바인딩 프로세스는 플러그형 서비스에 의해 제어 됩니다 **IActionValueBinder**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-208">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="b89f0-209">기본 구현은 **IActionValueBinder** 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-209">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="b89f0-210">검색할는 **ParameterBindingAttribute** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-210">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="b89f0-211">여기에 **[FromBody]**, **[FromUri]**, 및 **[ModelBinder]**, 또는 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-211">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="b89f0-212">그렇지 않으면, 찾는 위치 **HttpConfiguration.ParameterBindingRules** null이 아닌 반환 하는 함수에 대 한 **HttpParameterBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-212">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="b89f0-213">그렇지 않으면 이전에 설명 되어 있는 기본 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-213">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="b89f0-214">매개 변수 형식이 "단순" 형식 변환기가 있는 경우에 URI에서 바인딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="b89f0-214">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="b89f0-215">배치 같습니다는 **[FromUri]** 매개 변수에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-215">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="b89f0-216">그렇지 않은 경우 메시지 본문에서 매개 변수를 읽고 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-216">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="b89f0-217">배치 같습니다 **[FromBody]** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-217">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="b89f0-218">원하는 경우 전체를 바꿀 수 있습니다 **IActionValueBinder** 서비스 사용자 지정 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b89f0-218">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b89f0-219">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b89f0-219">Additional Resources</span></span>

[<span data-ttu-id="b89f0-220">사용자 지정 매개 변수 바인딩 예제</span><span class="sxs-lookup"><span data-stu-id="b89f0-220">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="b89f0-221">Mike Stall 웹 API 매개 변수 바인딩에 대 한 좋은 일련의 블로그 게시물을 작성:</span><span class="sxs-lookup"><span data-stu-id="b89f0-221">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="b89f0-222">매개 변수 바인딩 웹 API을 수행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b89f0-222">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="b89f0-223">웹 API에 대 한 MVC 스타일 매개 변수 바인딩</span><span class="sxs-lookup"><span data-stu-id="b89f0-223">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="b89f0-224">작업 서명은 MVC/웹 API에서의 사용자 지정 개체에 바인딩하는 방법</span><span class="sxs-lookup"><span data-stu-id="b89f0-224">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="b89f0-225">Web API에서 사용자 지정 값 공급자를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b89f0-225">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="b89f0-226">내부에서 web API 매개 변수 바인딩</span><span class="sxs-lookup"><span data-stu-id="b89f0-226">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
