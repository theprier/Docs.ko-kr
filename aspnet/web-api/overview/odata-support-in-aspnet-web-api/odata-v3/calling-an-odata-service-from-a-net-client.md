---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: ".NET 클라이언트 (C#)에서 OData 서비스를 호출할 | Microsoft Docs"
author: MikeWasson
description: "이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. (Visual S 인 works.. 자습서 Visual Studio 2013에서 사용 되는 소프트웨어 버전"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/26/2014
ms.topic: article
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: f6266045ebf55fb7ae691bfb55e9c90cd4edcc96
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="21f90-104">.NET 클라이언트 (C#)에서 OData 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-104">Calling an OData Service From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="21f90-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="21f90-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="21f90-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="21f90-107">이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="21f90-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="21f90-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="21f90-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012를 사용한 작동)</span><span class="sxs-lookup"><span data-stu-id="21f90-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="21f90-110">WCF Data Services 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="21f90-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/en-us/library/cc668772.aspx)
> - <span data-ttu-id="21f90-111">Web API 2입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-111">Web API 2.</span></span> <span data-ttu-id="21f90-112">(Web API 2를 사용 하 여 OData 서비스 예제 빌드될 있지만 클라이언트 응용 프로그램 웹 API에 의존 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="21f90-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>


<span data-ttu-id="21f90-113">이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 만드는 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="21f90-114">OData 서비스는 다음과 같은 엔터티를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="21f90-115">다음 문서에는 Web API에서 OData 서비스를 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="21f90-116">하지만 (않아도이 자습서에서는 이해를 읽을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="21f90-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="21f90-117">Web API 2 OData 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="21f90-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="21f90-118">Web API 2 OData 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="21f90-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="21f90-119">Web API 2 OData 작업</span><span class="sxs-lookup"><span data-stu-id="21f90-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="21f90-120">서비스 프록시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-120">Generate the Service Proxy</span></span>

<span data-ttu-id="21f90-121">서비스 프록시를 생성 하는 첫 번째 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="21f90-122">서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="21f90-123">프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="21f90-124">Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="21f90-125">IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + f 5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="21f90-126">Visual Studio 할당 하는 포트 번호를 포함 하 여 로컬 주소를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="21f90-127">프록시를 만들 때이 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="21f90-128">다음으로 Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="21f90-129">콘솔 응용 프로그램에는 OData 클라이언트 응용 프로그램이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-129">The console application will be our OData client application.</span></span> <span data-ttu-id="21f90-130">(또한 추가할 수 프로젝트는 서비스와 동일한 솔루션.)</span><span class="sxs-lookup"><span data-stu-id="21f90-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="21f90-131">나머지 단계 콘솔 프로젝트를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="21f90-131">The remaining steps refer the console project.</span></span>


<span data-ttu-id="21f90-132">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **참조** 선택 **서비스 참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="21f90-133">에 **서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="21f90-134">여기서 *포트* 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="21f90-135">에 대 한 **Namespace**, "ProductService"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="21f90-136">이 옵션 프록시 클래스의 네임 스페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="21f90-137">**찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-137">Click **Go**.</span></span> <span data-ttu-id="21f90-138">Visual Studio를 서비스에서 엔터티를 검색 하는 OData 메타 데이터 문서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="21f90-139">클릭 **확인** 프로젝트에 프록시 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="21f90-140">서비스 프록시 클래스의 인스턴스를 만들으십시오</span><span class="sxs-lookup"><span data-stu-id="21f90-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="21f90-141">내부 프로그램 `Main` 메서드를 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="21f90-142">를 사용 하 여 실제 포트 번호 프로그램 서비스가 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="21f90-143">서비스를 배포 하면 라이브 서비스의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="21f90-144">프록시를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="21f90-145">다음 코드는 요청 Uri를 콘솔 창에 출력 하는 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="21f90-146">이 단계 필요, 아니지만 각 쿼리에 대 한 Uri 참조를 보면 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="21f90-147">쿼리 서비스</span><span class="sxs-lookup"><span data-stu-id="21f90-147">Query the Service</span></span>

<span data-ttu-id="21f90-148">다음 코드는 OData 서비스에서 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="21f90-149">확인할 HTTP 요청을 보내거나 응답을 구문 분석을 위해 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="21f90-150">프록시 클래스는 자동으로 열거 하는 `Container.Products` 컬렉션에는 **foreach** 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="21f90-151">응용 프로그램을 실행 하면 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="21f90-152">ID에 따라 엔터티를 가져오려면는 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="21f90-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="21f90-153">이 항목의 나머지 부분에 대 한 전체 소개 하지 `Main` 서비스를 호출 하는 데 필요한 코드만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="21f90-154">쿼리 옵션을 적용</span><span class="sxs-lookup"><span data-stu-id="21f90-154">Apply Query Options</span></span>

<span data-ttu-id="21f90-155">OData 정의 [쿼리 옵션](../supporting-odata-query-options.md) 필터, 정렬, 페이지 데이터 등을 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="21f90-156">서비스 프록시를 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="21f90-157">이 섹션에서는 간단한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="21f90-158">자세한 내용은 항목을 참조 하십시오. [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/en-us/library/ee622463.aspx) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/en-us/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="21f90-159">필터링 ($filter)</span><span class="sxs-lookup"><span data-stu-id="21f90-159">Filtering ($filter)</span></span>

<span data-ttu-id="21f90-160">필터링 하려면 사용을 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="21f90-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="21f90-161">다음 예제 필터 제품 범주별으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="21f90-162">이 코드는 다음 OData 쿼리에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="21f90-163">프록시 변환에 `where` OData 절 `$filter` 식입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="21f90-164">정렬 ($orderby)</span><span class="sxs-lookup"><span data-stu-id="21f90-164">Sorting ($orderby)</span></span>

<span data-ttu-id="21f90-165">를 정렬 하려면 사용 하 여 프로그램 `orderby` 절.</span><span class="sxs-lookup"><span data-stu-id="21f90-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="21f90-166">다음 예제에서는 가격별 내림차순으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="21f90-167">다음은 해당 OData 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="21f90-168">클라이언트 쪽 페이징 ($skip 및 $top)</span><span class="sxs-lookup"><span data-stu-id="21f90-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="21f90-169">큰 엔터티 집합에 대 한 클라이언트는 결과의 수를 제한 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="21f90-170">예를 들어 클라이언트는 한 번에 10 개의 항목을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="21f90-171">이 라고 *클라이언트 쪽 페이징*합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-171">This is called *client-side paging*.</span></span> <span data-ttu-id="21f90-172">(또한 [서버 쪽 페이징](../supporting-odata-query-options.md#server-paging), 서버에서 결과의 수를 제한 하는 위치입니다.) LINQ를 사용 하 여 클라이언트 쪽 페이징을 수행 하려면 **Skip** 및 **걸릴** 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="21f90-173">다음 예제에서는 처음 40 결과 건너뛰고 10을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="21f90-174">다음은 해당 OData 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="21f90-175">Select ($select) 및 확장 ($expand)</span><span class="sxs-lookup"><span data-stu-id="21f90-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="21f90-176">사용 하 여 관련된 엔터티를 포함 하려면는 `DataServiceQuery<t>.Expand` 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="21f90-177">예를 들어, 포함 하는 `Supplier` 각 `Product`:</span><span class="sxs-lookup"><span data-stu-id="21f90-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="21f90-178">다음은 해당 OData 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="21f90-179">LINQ를 사용 하 여 응답의 셰이프를 변경 하려면 **선택** 절.</span><span class="sxs-lookup"><span data-stu-id="21f90-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="21f90-180">다음 예제에서는 다른 속성이 없는 각 제품의 이름만을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="21f90-181">다음은 해당 OData 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="21f90-182">Select 절 관련된 엔터티를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-182">A select clause can include related entities.</span></span> <span data-ttu-id="21f90-183">이 경우 호출 하지 않으면 **확장**; 프록시를 자동으로 포함 확장이 경우.</span><span class="sxs-lookup"><span data-stu-id="21f90-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="21f90-184">다음 예제에서는 이름 및 각 제품의 공급 업체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="21f90-185">다음은 해당 OData 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="21f90-186">여기에 포함 됩니다는 **$expand** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="21f90-187">$Select 및 $에 대 한 자세한 내용은 확장 하 고, 참조 [$select을 사용 하 여 $expand, 및 Web API 2에 $value](../using-select-expand-and-value.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="21f90-188">새 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="21f90-188">Add a New Entity</span></span>

<span data-ttu-id="21f90-189">엔터티 집합에 새 엔터티를 추가 하려면 `AddToEntitySet`여기서 *EntitySet* 엔터티 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="21f90-190">예를 들어 `AddToProducts` 를 새로 추가 `Product` 에 `Products` 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="21f90-191">프록시를 생성 하면 WCF 데이터 서비스를 자동으로 만듭니다 이러한 강력한 형식의 **AddTo** 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="21f90-192">두 엔터티 간의 링크를 추가 하려면 사용 된 **AddLink** 및 **SetLink** 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="21f90-193">다음 코드 새 공급 업체를 추가 하는 새 제품을 한 다음 간의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="21f90-194">사용 하 여 **AddLink** 때 탐색 속성은 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="21f90-195">이 예제에서는 제품을 추가 하 고는 `Products` 는 공급 업체에 대 한 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="21f90-196">사용 하 여 **SetLink** 때 탐색 속성은 단일 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="21f90-197">이 예제에서는 설정는 `Supplier` 제품에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="21f90-198">업데이트/패치</span><span class="sxs-lookup"><span data-stu-id="21f90-198">Update / Patch</span></span>

<span data-ttu-id="21f90-199">엔터티를 업데이트 하려면 호출는 **UpdateObject** 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="21f90-200">호출 하면 업데이트가 수행 되 **SaveChanges**합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="21f90-201">기본적으로 WCF HTTP MERGE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="21f90-202">**PatchOnUpdate** 옵션 대신 HTTP PATCH 보낼 WCF에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="21f90-203">병합 및 패치 이유?</span><span class="sxs-lookup"><span data-stu-id="21f90-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="21f90-204">원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) "부분 업데이트" 의미 체계를 사용 하 여 HTTP 메서드를 정의 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="21f90-205">부분 업데이트를 지원 하기는 OData 사양 MERGE 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="21f90-206">2010에서 [RFC 5789](http://tools.ietf.org/html/rfc5789) 부분 업데이트에 대 한 패치 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="21f90-207">이 기록의 일부를 읽을 수 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) WCF Data Services 블로그에서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="21f90-208">오늘날 패치 보다 선호 됩니다 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="21f90-209">Web API 스 캐 폴딩으로 만들어진 OData 컨트롤러 두 방법 모두를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>


<span data-ttu-id="21f90-210">전체 엔터티 (PUT 의미 체계가 아님)를 대체 하려면 지정 된 **ReplaceOnUpdate** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="21f90-211">이렇게 하면 WCF HTTP PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="21f90-212">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="21f90-212">Delete an Entity</span></span>

<span data-ttu-id="21f90-213">엔터티를 삭제 하려면 호출 **DeleteObject**합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="21f90-214">OData 작업을 호출</span><span class="sxs-lookup"><span data-stu-id="21f90-214">Invoke an OData Action</span></span>

<span data-ttu-id="21f90-215">Odata에서 [동작](odata-actions.md) 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="21f90-216">프록시 클래스는 OData 메타 데이터 문서 작업을 설명 하지만 하는 강력한 형식의 메서드 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="21f90-217">제네릭을 사용 하 여 OData 작업을 실행할 수 있습니다 **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="21f90-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="21f90-218">그러나 매개 변수 및 반환 값의 데이터 형식을 알고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="21f90-219">예를 들어는 `RateProduct` "등급" 형식의 명명 된 매개 변수를 사용 하는 작업 `Int32` 반환는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="21f90-220">다음 코드에는이 작업을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="21f90-221">자세한 내용은 참조[서비스 작업 호출 및 작업](https://msdn.microsoft.com/en-us/library/hh230677.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/en-us/library/hh230677.aspx).</span></span>

<span data-ttu-id="21f90-222">확장 하는 한 가지 방법은 **컨테이너** 작업을 호출 하는 강력한 형식의 메서드를 제공 하기 위해 클래스:</span><span class="sxs-lookup"><span data-stu-id="21f90-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
