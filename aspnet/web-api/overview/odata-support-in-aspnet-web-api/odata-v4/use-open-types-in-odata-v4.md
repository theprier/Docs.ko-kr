---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API 사용 하 여 OData v4의는 개방형 형식만 | Microsoft Docs
author: microsoft
description: OData v4의 개방형 형식 stuctured 있는 형식인 형식 정의에서 선언 된 속성 외에 동적 속성을 포함 합니다. 열기...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 77771d85532b8b622c2ad4ca219a38990e474c9c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838743"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="62c89-104">ASP.NET Web API 사용 하 여 OData v4의 종류를 열려면</span><span class="sxs-lookup"><span data-stu-id="62c89-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="62c89-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="62c89-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="62c89-106">OData v4의는 *형식을 열* stuctured 형식이 형식 정의에서 선언 된 속성 외에 동적 속성을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="62c89-107">개방형 형식 데이터 모델에 유연성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="62c89-108">이 자습서에서는 ASP.NET Web API OData의 개방형 형식을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="62c89-109">이 자습서에서는 ASP.NET Web API에서 OData 끝점을 만드는 방법을 이미 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="62c89-110">그렇지 않은 경우 먼저 읽으십시오 [OData v4 엔드포인트 만들기](create-an-odata-v4-endpoint.md) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="62c89-111">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="62c89-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="62c89-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="62c89-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="62c89-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="62c89-113">OData v4</span></span>


<span data-ttu-id="62c89-114">먼저 몇 가지 OData 용어:</span><span class="sxs-lookup"><span data-stu-id="62c89-114">First, some OData terminology:</span></span>

- <span data-ttu-id="62c89-115">엔터티 형식: 키를 사용 하 여 구조화 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="62c89-116">복합 형식: 키가 없는 구조적된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="62c89-117">Open 형식: 동적 속성을 사용 하 여 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="62c89-118">엔터티 형식 및 복합 형식 모두 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="62c89-119">기본 형식, 복합 형식 또는 열거형 형식; 동적 속성의 값 수 있습니다. 또는 이러한 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="62c89-120">개방형 형식에 대 한 자세한 내용은 참조는 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="62c89-121">웹 OData 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="62c89-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="62c89-122">NuGet 패키지 관리자를 사용 하 여 최신 Web API OData 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="62c89-123">패키지 관리자 콘솔 창:</span><span class="sxs-lookup"><span data-stu-id="62c89-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="62c89-124">CLR 유형 정의</span><span class="sxs-lookup"><span data-stu-id="62c89-124">Define the CLR Types</span></span>

<span data-ttu-id="62c89-125">CLR 형식과 EDM 모델을 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="62c89-126">(EDM (엔터티 데이터 모델) 만들어질 때</span><span class="sxs-lookup"><span data-stu-id="62c89-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="62c89-127">`Category` 열거형 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="62c89-128">`Address` 복합 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-128">`Address` is a complex type.</span></span> <span data-ttu-id="62c89-129">(이 없으므로 키를 엔터티 형식이 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="62c89-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="62c89-130">`Customer` 엔터티 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-130">`Customer` is an entity type.</span></span> <span data-ttu-id="62c89-131">(키가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="62c89-131">(It has a key.)</span></span>
- <span data-ttu-id="62c89-132">`Press` 열기 복합 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="62c89-133">`Book` 개방형 엔터티 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="62c89-134">만들려면 개방형 형식, CLR 형식 있어야 형식의 속성 `IDictionary<string, object>`, 동적 속성을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="62c89-135">EDM 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="62c89-135">Build the EDM Model</span></span>

<span data-ttu-id="62c89-136">사용 하는 경우 **ODataConventionModelBuilder** EDM을 만들려면 `Press` 하 고 `Book` 의 유무에 따라 열기 형식으로 자동으로 추가 됩니다을 `IDictionary<string, object>` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="62c89-137">빌드할 수도 있습니다 EDM 명시적으로 사용 하 여 **된 ODataModelBuilder**합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="62c89-138">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="62c89-138">Add an OData Controller</span></span>

<span data-ttu-id="62c89-139">다음으로, OData 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-139">Next, add an OData controller.</span></span> <span data-ttu-id="62c89-140">이 자습서에서는 지원 가져오기 및 게시를 요청 하는 메모리 내 목록을 사용 하 여 엔터티를 저장 하는 간소화 된 컨트롤러를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="62c89-141">첫 번째 `Book` 인스턴스에 동적 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="62c89-142">두 번째 `Book` 인스턴스는 동적 속성은:</span><span class="sxs-lookup"><span data-stu-id="62c89-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="62c89-143">"게시 됨": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="62c89-143">"Published": Primitive type</span></span>
- <span data-ttu-id="62c89-144">"작성자": 기본 형식의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="62c89-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="62c89-145">"OtherCategories": 열거형 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="62c89-146">또한 합니다 `Press` 속성의 `Book` 인스턴스는 동적 속성은:</span><span class="sxs-lookup"><span data-stu-id="62c89-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="62c89-147">"Blog": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="62c89-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="62c89-148">"Address": 복합 형식</span><span class="sxs-lookup"><span data-stu-id="62c89-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="62c89-149">메타 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-149">Query the Metadata</span></span>

<span data-ttu-id="62c89-150">OData 메타 데이터 문서를 가져오려면에 GET 요청을 보냄 `~/$metadata`합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="62c89-151">응답 본문은 다음과 유사 하 게 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="62c89-152">메타 데이터 문서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="62c89-153">에 대 한는 `Book` 및 `Press` 형식의 경우 값을 `OpenType` 특성은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="62c89-154">합니다 `Customer` 및 `Address` 형식을이 특성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="62c89-155">`Book` 엔터티 형식은 세 가지 선언 된 속성: ISBN, 제목 및 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="62c89-156">OData 메타 데이터를 포함 하지 않습니다는 `Book.Properties` CLR 클래스에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="62c89-157">마찬가지로,는 `Press` 복합 형식에 선언 된 두 개의 속성만: 이름 및 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="62c89-158">메타 데이터가 포함 되지 않습니다는 `Press.DynamicProperties` CLR 클래스에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="62c89-159">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="62c89-159">Query an Entity</span></span>

<span data-ttu-id="62c89-160">책 ISBN 사용 하 여 "978-7356-7942-0-9" 같음를 가져오려면에 GET 요청을 보냄 `~/Books('978-0-7356-7942-9')`합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="62c89-161">응답 본문은 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-161">The response body should look similar to the following.</span></span> <span data-ttu-id="62c89-162">(더 쉽게 읽을 수 있도록 들여씁니다).</span><span class="sxs-lookup"><span data-stu-id="62c89-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="62c89-163">동적 속성에 선언 된 속성을 사용 하 여 인라인에 포함된 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="62c89-164">엔터티를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-164">POST an Entity</span></span>

<span data-ttu-id="62c89-165">책 엔터티를 추가 하려면 POST 요청을 보낼 `~/Books`합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="62c89-166">클라이언트 요청 페이로드의 동적 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="62c89-167">요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-167">Here is an example request.</span></span> <span data-ttu-id="62c89-168">"Price" 및 "게시 됨" 속성을 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="62c89-169">컨트롤러 메서드에서 중단점을 설정 하는 경우 Web API에 이러한 속성을 추가 되었음을 확인할 수 있습니다는 `Properties` 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="62c89-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="62c89-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="62c89-170">Additional Resources</span></span>

[<span data-ttu-id="62c89-171">OData 오픈 형식 샘플</span><span class="sxs-lookup"><span data-stu-id="62c89-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
