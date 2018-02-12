---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: "ASP.NET web API OData v4에서 형식을 열 | Microsoft Docs"
author: microsoft
description: "OData v4, 개방형 형식이 형식 정의에 선언 된 모든 속성과 함께 동적 속성을 포함 하는 stuctured 형식 이지만 열기..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/15/2014
ms.topic: article
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fe67b9a11a82b55d5f3e0e5f1b0cee10a58833d2
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="e289f-104">ASP.NET web API OData v4에서 형식을 열합니다</span><span class="sxs-lookup"><span data-stu-id="e289f-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="e289f-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e289f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e289f-106">OData v 4에는 *형식을 열* stuctured 형식이 형식 정의에 선언 된 모든 속성과 함께 동적 속성을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="e289f-107">개방형 형식이 데이터 모델에 유연성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="e289f-108">이 자습서에는 ASP.NET Web API OData에서 열기 형식을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="e289f-109">이 자습서를 ASP.NET Web API에서 OData 끝점을 만드는 방법을 이미 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="e289f-110">그렇지 않은 경우 먼저 읽으십시오 [OData v4 끝점을 만드는](create-an-odata-v4-endpoint.md) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e289f-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="e289f-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e289f-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="e289f-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="e289f-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="e289f-113">OData v4</span></span>


<span data-ttu-id="e289f-114">첫째, 몇 가지 OData 용어:</span><span class="sxs-lookup"><span data-stu-id="e289f-114">First, some OData terminology:</span></span>

- <span data-ttu-id="e289f-115">엔터티 형식: 키가 있는 구조적된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="e289f-116">복합 형식: 키가 없는 구조적된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="e289f-117">형식 열: 동적 속성을 가진 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="e289f-118">엔터티 형식 및 복합 형식 모두 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="e289f-119">기본 형식, 복합 형식 또는 열거형 형식; 동적 속성의 값 수 있습니다. 또는 이러한 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="e289f-120">개방형 형식에 대 한 자세한 내용은 참조는 [OData v4 사양의](http://www.odata.org/documentation/odata-version-4-0/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="e289f-121">웹 OData 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="e289f-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="e289f-122">NuGet 패키지 관리자를 사용 하 여 최신 Web API OData 라이브러리를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="e289f-123">패키지 관리자 콘솔 창:</span><span class="sxs-lookup"><span data-stu-id="e289f-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="e289f-124">CLR 유형 정의</span><span class="sxs-lookup"><span data-stu-id="e289f-124">Define the CLR Types</span></span>

<span data-ttu-id="e289f-125">CLR 형식으로 EDM 모델을 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="e289f-126">(EDM (엔터티 데이터 모델)를 만들 때</span><span class="sxs-lookup"><span data-stu-id="e289f-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="e289f-127">`Category`열거형 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="e289f-128">`Address`복합 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-128">`Address` is a complex type.</span></span> <span data-ttu-id="e289f-129">(것은 아닙니다 키를 엔터티 형식이 되기 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="e289f-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="e289f-130">`Customer`엔터티 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-130">`Customer` is an entity type.</span></span> <span data-ttu-id="e289f-131">(키를 포함 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e289f-131">(It has a key.)</span></span>
- <span data-ttu-id="e289f-132">`Press`개방형 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="e289f-133">`Book`열린 엔터티 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="e289f-134">만들려면 개방형 형식, CLR 형식이 있어야 형식의 속성이 `IDictionary<string, object>`, 동적 속성을 보유 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="e289f-135">EDM 모델을 작성</span><span class="sxs-lookup"><span data-stu-id="e289f-135">Build the EDM Model</span></span>

<span data-ttu-id="e289f-136">사용 하는 경우 **ODataConventionModelBuilder** EDM 만들려는 `Press` 및 `Book` 의 존재 여부에 따라 개방형 형식으로 자동으로 추가 됩니다 한 `IDictionary<string, object>` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="e289f-137">빌드할 수도 있습니다는 EDM 명시적으로 사용 하 여 **된**합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="e289f-138">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="e289f-138">Add an OData Controller</span></span>

<span data-ttu-id="e289f-139">다음을 위해 OData 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-139">Next, add an OData controller.</span></span> <span data-ttu-id="e289f-140">이 자습서에서는 있는 정당한 지원 GET POST 요청, 업데이트 및 메모리에 목록을 사용 하 여 엔터티를 저장 하는 간소화 된 컨트롤러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="e289f-141">첫 번째 `Book` 인스턴스는 동적 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="e289f-142">두 번째 `Book` 인스턴스에 동적 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="e289f-143">"게시": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="e289f-143">"Published": Primitive type</span></span>
- <span data-ttu-id="e289f-144">"작성자": 기본 형식의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="e289f-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="e289f-145">"OtherCategories": 열거형 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="e289f-146">또한는 `Press` 속성의 `Book` 인스턴스는 동적 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="e289f-147">"블로그": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="e289f-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="e289f-148">"Address": 복합 형식</span><span class="sxs-lookup"><span data-stu-id="e289f-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="e289f-149">메타 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="e289f-149">Query the Metadata</span></span>

<span data-ttu-id="e289f-150">OData 메타 데이터 문서를 가져오려면에 GET 요청을 보내고 `~/$metadata`합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="e289f-151">응답 본문은 다음과 유사 하 게 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="e289f-152">메타 데이터 문서에서을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="e289f-153">에 대 한는 `Book` 및 `Press` 형식, 값은 `OpenType` 특성은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="e289f-154">`Customer` 및 `Address` 형식이이 특성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="e289f-155">`Book` 엔터티 형식에 선언 된 속성을 3 개의: ISBN, 제목 및 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="e289f-156">OData 메타 데이터 포함 되지 않습니다는 `Book.Properties` CLR 클래스에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="e289f-157">마찬가지로,는 `Press` 복합 형식에 선언 된 두 개의 속성: 이름 및 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="e289f-158">메타 데이터가 포함 되지 않습니다는 `Press.DynamicProperties` CLR 클래스에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="e289f-159">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="e289f-159">Query an Entity</span></span>

<span data-ttu-id="e289f-160">책 ISBN와 같은 "978-0-7356-7942-9"을 가져오려면에 GET 요청을 보내고 `~/Books('978-0-7356-7942-9')`합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="e289f-161">응답 본문은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-161">The response body should look similar to the following.</span></span> <span data-ttu-id="e289f-162">들여쓰기 더 쉽게 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="e289f-163">동적 속성에 선언 된 속성에 인라인으로 포함된 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="e289f-164">엔터티를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-164">POST an Entity</span></span>

<span data-ttu-id="e289f-165">POST 요청을 보내기는 Book 엔터티를 추가 하려면 `~/Books`합니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="e289f-166">클라이언트 요청 페이로드에 동적 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="e289f-167">다음은 예제 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-167">Here is an example request.</span></span> <span data-ttu-id="e289f-168">Note "Price" 및 "게시" 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="e289f-169">컨트롤러 메서드에서 중단점을 설정한 경우이 속성에 추가 된 웹 API 확인할 수 있습니다는 `Properties` 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="e289f-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="e289f-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e289f-170">Additional Resources</span></span>

[<span data-ttu-id="e289f-171">OData 열기 형식 샘플</span><span class="sxs-lookup"><span data-stu-id="e289f-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
