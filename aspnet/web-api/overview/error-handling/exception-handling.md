---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API의에서 예외 처리 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2012
ms.topic: article
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: c65ddcca012840d70ab5a33af92edb30041be971
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506962"
---
<a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="3f4e2-102">ASP.NET Web API의에서 예외 처리</span><span class="sxs-lookup"><span data-stu-id="3f4e2-102">Exception Handling in ASP.NET Web API</span></span>
====================
<span data-ttu-id="3f4e2-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3f4e2-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3f4e2-104">이 문서에서는 오류 및 ASP.NET Web API의 예외 처리를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="3f4e2-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="3f4e2-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="3f4e2-106">예외 필터</span><span class="sxs-lookup"><span data-stu-id="3f4e2-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="3f4e2-107">예외 필터를 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="3f4e2-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="3f4e2-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="3f4e2-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="3f4e2-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="3f4e2-109">HttpResponseException</span></span>

<span data-ttu-id="3f4e2-110">Web API 컨트롤러 확인할 수 없는 예외를 throw 하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="3f4e2-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="3f4e2-111">기본적으로 대부분의 예외는 상태 코드 500 내부 서버 오류와 함께 HTTP 응답으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="3f4e2-112">**HttpResponseException** 형식은 특수 한 경우.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="3f4e2-113">이 예외는 예외 생성자에서 지정 하는 모든 HTTP 상태 코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="3f4e2-114">경우 404 찾을 수 없는 다음 메서드 반환 하는 예를 들어는 *id* 매개 변수가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="3f4e2-115">응답 보다 자세히 제어 수도 전체 응답 메시지를 생성 하 고 사용 하 여 포함 된 **HttpResponseException:**</span><span class="sxs-lookup"><span data-stu-id="3f4e2-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="3f4e2-116">예외 필터</span><span class="sxs-lookup"><span data-stu-id="3f4e2-116">Exception Filters</span></span>

<span data-ttu-id="3f4e2-117">웹 API를 작성 하 여 예외를 처리 하는 방법을 사용자 지정할 수는 *예외 필터*합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="3f4e2-118">예외 필터는 컨트롤러 메서드를 한 처리 되지 않은 예외를 throw 될 때 실행 되 *하지* 는 **HttpResponseException** 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="3f4e2-119">**HttpResponseException** 형식이 특별 한 경우 반환 된 HTTP 응답에 대 한 구체적으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="3f4e2-120">예외 필터를 구현에서 **System.Web.Http.Filters.IExceptionFilter** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="3f4e2-121">파생 하는 예외 필터 작성 하는 가장 간단한 방법은 **System.Web.Http.Filters.ExceptionFilterAttribute** 클래스 및 재정의 **OnException** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="3f4e2-122">ASP.NET Web API의 예외 필터는 ASP.NET MVC의 경우와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="3f4e2-123">그러나 선언 된 함수 및 별도 네임 스페이스에 개별적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="3f4e2-124">특히는 **HandleErrorAttribute** MVC에서 사용 되는 클래스는 Web API 컨트롤러에서 발생 한 예외를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>


<span data-ttu-id="3f4e2-125">다음으로 변환 하는 필터를은 **NotImplementedException** 예외가 HTTP 상태 코드 501 구현 되지 않음:</span><span class="sxs-lookup"><span data-stu-id="3f4e2-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="3f4e2-126">**응답** 의 속성은 **HttpActionExecutedContext** 클라이언트에 전송 될 HTTP 응답 메시지를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="3f4e2-127">예외 필터를 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="3f4e2-127">Registering Exception Filters</span></span>

<span data-ttu-id="3f4e2-128">웹 API 예외 필터를 등록 하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="3f4e2-129">작업에 의해</span><span class="sxs-lookup"><span data-stu-id="3f4e2-129">By action</span></span>
- <span data-ttu-id="3f4e2-130">컨트롤러에 의해</span><span class="sxs-lookup"><span data-stu-id="3f4e2-130">By controller</span></span>
- <span data-ttu-id="3f4e2-131">전역으로</span><span class="sxs-lookup"><span data-stu-id="3f4e2-131">Globally</span></span>

<span data-ttu-id="3f4e2-132">특정 작업에 필터를 적용할 필터 특성으로 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="3f4e2-133">모든 컨트롤러에서 작업 하는 필터를 적용 하려면 필터 특성으로 컨트롤러 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="3f4e2-134">필터를 적용 하려면 전역적으로 모든 Web API 컨트롤러에 추가 필터의 인스턴스는 **GlobalConfiguration.Configuration.Filters** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="3f4e2-135">이 컬렉션의 예외 필터는 모든 Web API 컨트롤러 작업에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-135">Exeption filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="3f4e2-136">"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만드는 경우 내부 웹 API 구성 코드를 입력의 `WebApiConfig` 응용 프로그램에 있는 클래스\_시작 폴더:</span><span class="sxs-lookup"><span data-stu-id="3f4e2-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="3f4e2-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="3f4e2-137">HttpError</span></span>

<span data-ttu-id="3f4e2-138">**HttpError** 개체 응답 본문에 오류 정보를 반환 하는 일관 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="3f4e2-139">다음 예제와 HTTP 상태 코드 404 (찾을 수 없음)를 반환 하는 방법을 보여 줍니다.는 **HttpError** 응답 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="3f4e2-140">**CreateErrorResponse** 에 정의 된 확장 메서드는 **System.Net.Http.HttpRequestMessageExtensions** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="3f4e2-141">내부적으로 **CreateErrorResponse** 만듭니다는 **HttpError** 인스턴스 한 다음 만듭니다는 **HttpResponseMessage** 를 포함 하는 **HttpError**.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="3f4e2-142">메서드가 성공 하면이 예제에서는 제품 HTTP 응답에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="3f4e2-143">요청 된 제품 없으면 HTTP 응답에 포함 되어 있지만 **HttpError** 요청 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="3f4e2-144">응답 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="3f4e2-145">에 **HttpError** 이 예제 JSON으로 serialize 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="3f4e2-146">사용 하 여의 장점 중 하나 **HttpError** 동일한를 통해 이동 하는지는 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md) 다른 강력한 형식의 모델을 처리 하는 serialization 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="3f4e2-147">HttpError 및 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3f4e2-147">HttpError and Model Validation</span></span>

<span data-ttu-id="3f4e2-148">모델 유효성 검사에 대 한 모델 상태를 전달할 수 있습니다 **CreateErrorResponse**응답의 유효성 검사 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="3f4e2-149">이 예에서는 다음 응답을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="3f4e2-150">모델 유효성 검사에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="3f4e2-151">HttpResponseException HttpError 사용</span><span class="sxs-lookup"><span data-stu-id="3f4e2-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="3f4e2-152">앞의 예제에서는 반환는 **HttpResponseMessage** 컨트롤러 작업에서 메시지를 사용할 수도 **HttpResponseException** 반환 하는 **HttpError**합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4e2-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="3f4e2-153">이렇게 하면 여전히 반환 하는 동안 일반 성공의 경우 강력한 형식의 모델이 반환 **HttpError** 오류가 발생 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3f4e2-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
