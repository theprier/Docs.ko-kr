---
title: "ASP.NET Core MVC 웹 API의 사용자 지정 포맷터"
author: tdykstra
description: "ASP.NET Core의 웹 API에서 사용자 지정 포맷터를 만들고 사용하는 방법을 알아봅니다."
manager: wpickett
ms.author: tdykstra
ms.date: 02/08/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/models/custom-formatters
ms.openlocfilehash: 8a42f2d885bd0a0c6d2bd05f9c589def2e15d50a
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="custom-formatters-in-aspnet-core-mvc-web-apis"></a><span data-ttu-id="ea769-103">ASP.NET Core MVC 웹 API의 사용자 지정 포맷터</span><span class="sxs-lookup"><span data-stu-id="ea769-103">Custom formatters in ASP.NET Core MVC web APIs</span></span>

<span data-ttu-id="ea769-104">작성자: [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ea769-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="ea769-105">ASP.NET Core MVC는 JSON, XML 또는 일반 텍스트 형식을 사용하여 웹 API에서 데이터 교환에 대한 기본 제공 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-105">ASP.NET Core MVC has built-in support for data exchange in web APIs by using JSON, XML, or plain text formats.</span></span> <span data-ttu-id="ea769-106">이 문서에서는 사용자 지정 포맷터를 만들어 추가 형식에 대한 지원을 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-106">This article shows how to add support for additional formats by creating custom formatters.</span></span>

<span data-ttu-id="ea769-107">[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample)</span><span class="sxs-lookup"><span data-stu-id="ea769-107">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span></span>

## <a name="when-to-use-custom-formatters"></a><span data-ttu-id="ea769-108">사용자 지정 포맷터를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="ea769-108">When to use custom formatters</span></span>

<span data-ttu-id="ea769-109">[콘텐츠 협상](xref:mvc/models/formatting) 프로세스에서 기본 제공 포맷터에 의해 지원되지 않는 콘텐츠 형식을 지원하려는 경우(JSON, XML 및 일반 텍스트) 사용자 지정 포맷터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-109">Use a custom formatter when you want the [content negotiation](xref:mvc/models/formatting) process to support a content type that isn't supported by the built-in formatters (JSON, XML, and plain text).</span></span>

<span data-ttu-id="ea769-110">예를 들어, 웹 API의 클라이언트 중 일부가 [Protobuf](https://github.com/google/protobuf) 형식을 처리할 수 있는 경우 더 효율적이기 때문에 해당 클라이언트에서 Protobuf를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-110">For example, if some of the clients for your web API can handle the [Protobuf](https://github.com/google/protobuf) format, you might want to use Protobuf with those clients because it's more efficient.</span></span>  <span data-ttu-id="ea769-111">또는 웹 API에서 연락 데이터를 교환하는 데 자주 사용되는 [vCard](https://wikipedia.org/wiki/VCard) 형식으로 연락처 이름 및 주소를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-111">Or you might want your web API to send contact names and addresses in [vCard](https://wikipedia.org/wiki/VCard) format, a commonly used format for exchanging contact data.</span></span> <span data-ttu-id="ea769-112">이 문서에서 제공하는 샘플 앱은 간단한 vCard 포맷터를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-112">The sample app provided with this article implements a simple vCard formatter.</span></span>

## <a name="overview-of-how-to-use-a-custom-formatter"></a><span data-ttu-id="ea769-113">사용자 지정 포맷터를 사용하는 방법 개요</span><span class="sxs-lookup"><span data-stu-id="ea769-113">Overview of how to use a custom formatter</span></span>

<span data-ttu-id="ea769-114">사용자 지정 포맷터를 만들고 사용하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-114">Here are the steps to create and use a custom formatter:</span></span>

* <span data-ttu-id="ea769-115">클라이언트에 보낼 데이터를 직렬화하려는 경우 출력 포맷터 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-115">Create an output formatter class if you want to serialize data to send to the client.</span></span>
* <span data-ttu-id="ea769-116">클라이언트에서 받을 데이터를 deserialize하려는 경우 입력 포맷터 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-116">Create an input formatter class if you want to deserialize data received from the client.</span></span> 
* <span data-ttu-id="ea769-117">포맷터의 인스턴스를 [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions)의 `InputFormatters` 및 `OutputFormatters` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-117">Add instances of your formatters to the `InputFormatters` and `OutputFormatters` collections in [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span></span>

<span data-ttu-id="ea769-118">다음 섹션에서는 이러한 각 단계에 대한 지침 및 코드 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-118">The following sections provide guidance and code examples for each of these steps.</span></span>

## <a name="how-to-create-a-custom-formatter-class"></a><span data-ttu-id="ea769-119">사용자 지정 포맷터 클래스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ea769-119">How to create a custom formatter class</span></span>

<span data-ttu-id="ea769-120">포맷터를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="ea769-120">To create a formatter:</span></span>

* <span data-ttu-id="ea769-121">적절한 기본 클래스에서 클래스를 파생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-121">Derive the class from the appropriate base class.</span></span>
* <span data-ttu-id="ea769-122">생성자에서 유효한 미디어 형식 및 인코딩을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-122">Specify valid media types and encodings in the constructor.</span></span>
* <span data-ttu-id="ea769-123">`CanReadType`/`CanWriteType` 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="ea769-123">Override `CanReadType`/`CanWriteType` methods</span></span>
* <span data-ttu-id="ea769-124">`ReadRequestBodyAsync`/`WriteResponseBodyAsync` 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="ea769-124">Override `ReadRequestBodyAsync`/`WriteResponseBodyAsync` methods</span></span>
  
### <a name="derive-from-the-appropriate-base-class"></a><span data-ttu-id="ea769-125">적절한 기본 클래스에서 파생</span><span class="sxs-lookup"><span data-stu-id="ea769-125">Derive from the appropriate base class</span></span>

<span data-ttu-id="ea769-126">텍스트 미디어 형식(예: vCard)의 경우 [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) 또는 [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) 기본 클래스에서 파생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-126">For text media types (for example, vCard), derive from the [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) or [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) base class.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

<span data-ttu-id="ea769-127">이진 형식의 경우 [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) 또는 [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) 기본 클래스에서 파생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-127">For binary types, derive from the [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) or [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) base class.</span></span>

### <a name="specify-valid-media-types-and-encodings"></a><span data-ttu-id="ea769-128">유효한 미디어 형식 및 인코딩 지정</span><span class="sxs-lookup"><span data-stu-id="ea769-128">Specify valid media types and encodings</span></span>

<span data-ttu-id="ea769-129">생성자에서 `SupportedMediaTypes` 및 `SupportedEncodings` 컬렉션에 추가하여 유효한 미디어 형식 및 인코딩을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-129">In the constructor, specify valid media types and encodings by adding to the `SupportedMediaTypes` and `SupportedEncodings` collections.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

> [!NOTE]  
> <span data-ttu-id="ea769-130">포맷터 클래스에서 생성자 종속성 주입을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-130">You can't do constructor dependency injection in a formatter class.</span></span> <span data-ttu-id="ea769-131">예를 들어 생성자에 로거 매개 변수를 추가하여 로거를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-131">For example, you can't get a logger by adding a logger parameter to the constructor.</span></span> <span data-ttu-id="ea769-132">서비스에 액세스하려면 메서드에 전달된 컨텍스트 개체를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-132">To access services, you have to use the context object that gets passed in to your methods.</span></span> <span data-ttu-id="ea769-133">[아래](#read-write) 코드 예제에서는 수행 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-133">A code example [below](#read-write) shows how to do this.</span></span>

### <a name="override-canreadtypecanwritetype"></a><span data-ttu-id="ea769-134">Override CanReadType/CanWriteType</span><span class="sxs-lookup"><span data-stu-id="ea769-134">Override CanReadType/CanWriteType</span></span> 

<span data-ttu-id="ea769-135">`CanReadType` 또는 `CanWriteType` 메서드를 재정의하여 deserialize하거나 직렬화할 수 있는 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-135">Specify the type you can deserialize into or serialize from by overriding the `CanReadType` or `CanWriteType` methods.</span></span> <span data-ttu-id="ea769-136">예를 들어 `Contact` 형식에서 vCard 텍스트를 만들거나 그 반대로 수행할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-136">For example, you might only be able to create vCard text from a `Contact` type and vice versa.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

#### <a name="the-canwriteresult-method"></a><span data-ttu-id="ea769-137">CanWriteResult 메서드</span><span class="sxs-lookup"><span data-stu-id="ea769-137">The CanWriteResult method</span></span>

<span data-ttu-id="ea769-138">일부 시나리오에서는 `CanWriteType` 대신 `CanWriteResult`를 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-138">In some scenarios you have to override `CanWriteResult` instead of `CanWriteType`.</span></span> <span data-ttu-id="ea769-139">다음 조건이 true인 경우 `CanWriteResult`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-139">Use `CanWriteResult` if the following conditions are true:</span></span>

  * <span data-ttu-id="ea769-140">작업 메서드에서는 모델 클래스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-140">Your action method returns a model class.</span></span>
  * <span data-ttu-id="ea769-141">런타임 시 반환될 수 있는 파생 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-141">There are derived classes which might be returned at runtime.</span></span>
  * <span data-ttu-id="ea769-142">런타임 시 작업에서 반환하는 파생 클래스를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-142">You need to know at runtime which derived class was returned by the action.</span></span>  

<span data-ttu-id="ea769-143">예를 들어 작업 메서드 서명이 `Person` 형식을 반환한다고 가정하지만 `Person`에서 파생된 `Student` 또는 `Instructor` 형식을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-143">For example, suppose your action method signature returns a `Person` type, but it may return a `Student` or `Instructor` type that derives from `Person`.</span></span> <span data-ttu-id="ea769-144">포맷터에서 `Student` 개체만을 처리하려는 경우 `CanWriteResult` 메서드에 제공된 컨텍스트 개체에서 [개체](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-144">If you want your formatter to handle only `Student` objects, check the type of [Object](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) in the context object provided to the `CanWriteResult` method.</span></span> <span data-ttu-id="ea769-145">작업 메서드가 `IActionResult`를 반환할 때 반드시 `CanWriteResult`를 사용해야 하는 것은 아닙니다. 이 경우에 `CanWriteType` 메서드는 런타임 형식을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-145">Note that it's not necessary to use `CanWriteResult` when the action method returns `IActionResult`; in that case, the `CanWriteType` method receives the runtime type.</span></span>

<a id="read-write"></a>
### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a><span data-ttu-id="ea769-146">ReadRequestBodyAsync/WriteResponseBodyAsync 재정의</span><span class="sxs-lookup"><span data-stu-id="ea769-146">Override ReadRequestBodyAsync/WriteResponseBodyAsync</span></span> 

<span data-ttu-id="ea769-147">`ReadRequestBodyAsync` 또는 `WriteResponseBodyAsync`에서 deserialize하거나 직렬화하는 작업의 실제 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-147">You do the actual work of deserializing or serializing in `ReadRequestBodyAsync` or `WriteResponseBodyAsync`.</span></span>  <span data-ttu-id="ea769-148">다음 예제에서 강조 표시된 줄은 종속성 주입 컨테이너에서 서비스를 가져오는 방법을 보여줍니다(생성자 매개 변수에서 가져올 수 없음).</span><span class="sxs-lookup"><span data-stu-id="ea769-148">The highlighted lines in the following example show how to get services from the dependency injection container (you can't get them from constructor parameters).</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a><span data-ttu-id="ea769-149">사용자 지정 포맷터를 사용하도록 MVC를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="ea769-149">How to configure MVC to use a custom formatter</span></span>
 
<span data-ttu-id="ea769-150">사용자 지정 포맷터를 사용하려면 `InputFormatters` 또는 `OutputFormatters` 컬렉션에 포맷터 클래스의 인스턴스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-150">To use a custom formatter, add an instance of the formatter class to the `InputFormatters` or `OutputFormatters` collection.</span></span>

[!code-csharp[Main](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

<span data-ttu-id="ea769-151">포맷터는 삽입한 순서 대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-151">Formatters are evaluated in the order you insert them.</span></span> <span data-ttu-id="ea769-152">첫 번째 포맷터가 우선됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-152">The first one takes precedence.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ea769-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea769-153">Next steps</span></span>

<span data-ttu-id="ea769-154">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample)을 참조하세요. 여기서는 간단한 vCard 입력 및 출력 포맷터를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-154">See the [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), which implements simple vCard input and output formatters.</span></span>  <span data-ttu-id="ea769-155">응용 프로그램은 다음 예제와 같이 vCard를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-155">The application reads and writes vCards that look like the following example:</span></span>

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

<span data-ttu-id="ea769-156">vCard 출력을 확인하려면 응용 프로그램을 실행하고 `http://localhost:63313/api/contacts/`(Visual Studio에서 실행할 때) 또는 `http://localhost:5000/api/contacts/`(명령줄에서 실행할 때)에 수락 헤더 "텍스트/vcard"를 포함하는 Get 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-156">To see vCard output, run the application and send a Get request with Accept header "text/vcard" to `http://localhost:63313/api/contacts/` (when running from Visual Studio) or `http://localhost:5000/api/contacts/` (when running from the command line).</span></span>

<span data-ttu-id="ea769-157">연락처의 메모리 내 컬렉션에 vCard를 추가하려면 콘텐츠 형식 헤더 "텍스트/vcard" 및 본문의 vCard 텍스트를 포함하는 위의 예제와 같은 형식으로 지정된 동일한 URL에 Post 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea769-157">To add a vCard to the in-memory collection of contacts, send a Post request to the same URL, with Content-Type header "text/vcard" and with vCard text in the body, formatted like the example above.</span></span>
