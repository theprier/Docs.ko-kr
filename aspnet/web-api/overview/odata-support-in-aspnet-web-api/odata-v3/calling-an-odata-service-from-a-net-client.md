---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET 클라이언트 (C#)에서 OData 서비스를 호출 합니다. | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. 자습서 Visual Studio 2013 (호환 Visual S....에 사용 되는 소프트웨어 버전
ms.author: aspnetcontent
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 72dca7dc2ec27f15c9f0526621a713267f5835f8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819557"
---
<a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="ea511-104">.NET 클라이언트 (C#)에서 OData 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-104">Calling an OData Service From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="ea511-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ea511-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ea511-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ea511-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="ea511-107">이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ea511-108">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ea511-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ea511-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012를 사용 하 여 작동)</span><span class="sxs-lookup"><span data-stu-id="ea511-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="ea511-110">WCF Data Services 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="ea511-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="ea511-111">Web API 2입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-111">Web API 2.</span></span> <span data-ttu-id="ea511-112">(예제에서는 OData 서비스 Web API 2를 사용 하 여 빌드됩니다. 하지만 클라이언트 응용 프로그램이 웹 API에 종속 되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="ea511-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>


<span data-ttu-id="ea511-113">이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 작성 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="ea511-114">OData 서비스는 다음 엔터티를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="ea511-115">다음 문서를 웹 API에서 OData 서비스를 구현 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="ea511-116">(필요가 있지만이 자습서에서는 이해 하기 읽을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ea511-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="ea511-117">Web API 2에서에서 OData 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="ea511-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="ea511-118">Web API 2 OData 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="ea511-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="ea511-119">Web API 2의 OData 작업</span><span class="sxs-lookup"><span data-stu-id="ea511-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="ea511-120">서비스 프록시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-120">Generate the Service Proxy</span></span>

<span data-ttu-id="ea511-121">첫 번째 단계는 서비스 프록시를 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="ea511-122">서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="ea511-123">프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="ea511-124">Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="ea511-125">IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="ea511-126">Visual Studio 할당 하는 포트 번호를 포함 하 여 로컬 주소를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="ea511-127">프록시를 만들 때이 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="ea511-128">다음으로, Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="ea511-129">콘솔 응용 프로그램에는 OData 클라이언트 응용 프로그램이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-129">The console application will be our OData client application.</span></span> <span data-ttu-id="ea511-130">(추가할 수 있습니다도 프로젝트 서비스와 동일한 솔루션에.)</span><span class="sxs-lookup"><span data-stu-id="ea511-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="ea511-131">나머지 단계를 콘솔 프로젝트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ea511-131">The remaining steps refer the console project.</span></span>


<span data-ttu-id="ea511-132">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **참조가** 선택한 **서비스 참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="ea511-133">에 **서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="ea511-134">여기서 *포트* 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="ea511-135">에 대 한 **Namespace**, "ProductService"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="ea511-136">이 옵션은 프록시 클래스의 네임 스페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="ea511-137">**찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-137">Click **Go**.</span></span> <span data-ttu-id="ea511-138">Visual Studio에는 서비스에서 엔터티를 검색할 OData 메타 데이터 문서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="ea511-139">클릭 **확인** 프로젝트에 프록시 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="ea511-140">서비스 프록시 클래스의 인스턴스를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="ea511-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="ea511-141">내부 프로그램 `Main` 메서드를 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="ea511-142">를 사용 하 여 실제 포트 번호를 서비스가 실행 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="ea511-143">서비스를 배포 하는 경우에 라이브 서비스의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="ea511-144">프록시를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="ea511-145">다음 코드는 콘솔 창에는 요청 Uri를 출력 하는 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="ea511-146">이 단계 필요 없지만 각 쿼리에 대 한 Uri를 확인 하려면 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="ea511-147">서비스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-147">Query the Service</span></span>

<span data-ttu-id="ea511-148">다음 코드는 OData 서비스에서 제품 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="ea511-149">HTTP 요청을 보내거나 응답을 구문 분석을 위해 어떠한 코드도 작성할 필요가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="ea511-150">프록시 클래스는 자동으로 열거 하는 `Container.Products` 컬렉션에는 **foreach** 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="ea511-151">응용 프로그램을 실행 하는 경우 출력은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="ea511-152">ID에 따라 엔터티를 가져오려면는 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="ea511-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="ea511-153">이 항목의 나머지 부분에 대 한 전체 소개 하지 `Main` 서비스를 호출 하는 데 필요한 코드에만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="ea511-154">쿼리 옵션을 적용</span><span class="sxs-lookup"><span data-stu-id="ea511-154">Apply Query Options</span></span>

<span data-ttu-id="ea511-155">OData는 정의 [쿼리 옵션](../supporting-odata-query-options.md) 필터, 정렬, 페이지 데이터 등을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="ea511-156">서비스 프록시에 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="ea511-157">이 섹션에서는 간단한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="ea511-158">자세한 내용은 항목을 참조 하세요 [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) MSDN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="ea511-159">필터링 ($filter)</span><span class="sxs-lookup"><span data-stu-id="ea511-159">Filtering ($filter)</span></span>

<span data-ttu-id="ea511-160">필터링에 사용 된 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="ea511-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="ea511-161">제품 범주에 따라 다음 예제에서는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="ea511-162">이 코드는 다음 OData 쿼리에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="ea511-163">프록시를 변환 하는 `where` OData 절 `$filter` 식입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="ea511-164">정렬 ($orderby)</span><span class="sxs-lookup"><span data-stu-id="ea511-164">Sorting ($orderby)</span></span>

<span data-ttu-id="ea511-165">정렬에 사용 하 여는 `orderby` 절.</span><span class="sxs-lookup"><span data-stu-id="ea511-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="ea511-166">다음 예제에서는 가격 최상위에서 최하위 순으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="ea511-167">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="ea511-168">클라이언트 쪽 페이징 ($skip 및 $top)</span><span class="sxs-lookup"><span data-stu-id="ea511-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="ea511-169">큰 엔터티 집합에 대 한 클라이언트 결과의 수를 제한 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="ea511-170">예를 들어, 클라이언트는 한 번에 10 개 항목을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="ea511-171">이 이라고 *클라이언트 쪽 페이징*합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-171">This is called *client-side paging*.</span></span> <span data-ttu-id="ea511-172">(이기도 [서버측 페이징이](../supporting-odata-query-options.md#server-paging), 서버에서 결과의 수를 제한 하는 위치입니다.) 클라이언트 쪽 페이징을 수행 하려면 LINQ를 사용 **Skip** 하 고 **걸릴** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="ea511-173">다음 예제는 처음 40 결과 건너뛰고 10을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="ea511-174">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="ea511-175">선택 ($select) 및 확장 ($expand)</span><span class="sxs-lookup"><span data-stu-id="ea511-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="ea511-176">관련된 엔터티를 포함 하려면 사용 된 `DataServiceQuery<t>.Expand` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="ea511-177">예를 들어 포함 된 `Supplier` 각각에 대해 `Product`:</span><span class="sxs-lookup"><span data-stu-id="ea511-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="ea511-178">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="ea511-179">LINQ를 사용 하 여 응답의 형태를 변경 하려면 **선택** 절.</span><span class="sxs-lookup"><span data-stu-id="ea511-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="ea511-180">다음 예제에서는 다른 속성이 없는 각 제품의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="ea511-181">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="ea511-182">Select 절 관련된 엔터티를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-182">A select clause can include related entities.</span></span> <span data-ttu-id="ea511-183">이 경우 호출 하지 마세요 **확장**; 프록시를 자동으로 포함 확장이 경우.</span><span class="sxs-lookup"><span data-stu-id="ea511-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="ea511-184">다음 예제에서는 각 제품의 공급 업체와 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="ea511-185">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="ea511-186">포함 하는 **$expand** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="ea511-187">$Select 및 $에 대 한 자세한 정보에 대 한 확장 참조 하세요 [$expand $select 사용 및 Web API 2에서 $value](../using-select-expand-and-value.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="ea511-188">새 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-188">Add a New Entity</span></span>

<span data-ttu-id="ea511-189">엔터티 집합에 새 엔터티를 추가할 호출 `AddToEntitySet`, 여기서 *EntitySet* 엔터티 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="ea511-190">예를 들어 `AddToProducts` 새 `Product` 에 `Products` 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="ea511-191">프록시를 생성 하면 WCF Data Services를 자동으로 만듭니다 이러한 강력한 **AddTo** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="ea511-192">두 엔터티 간의 링크를 추가 하려면 사용 합니다 **AddLink** 하 고 **SetLink** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="ea511-193">다음 코드는 새 공급 업체 및 새 제품을 추가 하 고 간의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="ea511-194">사용 하 여 **AddLink** 경우 탐색 속성이 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="ea511-195">이 예제에서는 제품을 추가 하 고는 `Products` 공급자의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="ea511-196">사용 하 여 **SetLink** 경우 탐색 속성은 단일 엔터티.</span><span class="sxs-lookup"><span data-stu-id="ea511-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="ea511-197">이 예제에서는 설정 된 것을 `Supplier` 제품에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="ea511-198">업데이트/패치</span><span class="sxs-lookup"><span data-stu-id="ea511-198">Update / Patch</span></span>

<span data-ttu-id="ea511-199">엔터티를 업데이트 하려면 호출을 **UpdateObject** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="ea511-200">호출 하는 경우 업데이트를 수행한 **SaveChanges**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="ea511-201">기본적으로 WCF는 HTTP MERGE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="ea511-202">**PatchOnUpdate** 옵션은 WCF는 HTTP PATCH를 대신 보낼에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="ea511-203">병합 및 패치는 이유?</span><span class="sxs-lookup"><span data-stu-id="ea511-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="ea511-204">원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) "부분 업데이트" 의미 체계를 사용 하 여 모든 HTTP 메서드를 정의 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="ea511-205">부분 업데이트를 지원 하려면 OData 사양을 MERGE 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="ea511-206">2010에서는 [RFC 5789](http://tools.ietf.org/html/rfc5789) 부분 업데이트에 대 한 PATCH 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="ea511-207">이 기록의 일부를 읽을 수 있습니다 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) WCF Data Services 블로그에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="ea511-208">현재 패치 보다 선호 됩니다 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="ea511-209">Web API 스 캐 폴딩을 통해 만든 OData 컨트롤러에는 두 방법 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>


<span data-ttu-id="ea511-210">전체 엔터티 (PUT 의미 체계가 아님)를 대체 하려는 경우 지정 된 **ReplaceOnUpdate** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="ea511-211">이렇게 하면 WCF는 HTTP PUT 요청을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="ea511-212">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="ea511-212">Delete an Entity</span></span>

<span data-ttu-id="ea511-213">엔터티를 삭제 하려면 호출 **DeleteObject**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="ea511-214">OData 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-214">Invoke an OData Action</span></span>

<span data-ttu-id="ea511-215">Odata에서 [작업](odata-actions.md) 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="ea511-216">프록시 클래스는 작업을 설명 하는 OData 메타 데이터 문서, 하지만에 강력한 형식의 메서드 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="ea511-217">제네릭 사용 하 여 OData 작업을 실행할 수 있습니다 **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ea511-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="ea511-218">그러나 매개 변수 및 반환 값의 데이터 형식을 알 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="ea511-219">예를 들어, 합니다 `RateProduct` "등급" 형식의 명명 된 매개 변수를 사용 하는 작업 `Int32` 반환을 `double`.</span><span class="sxs-lookup"><span data-stu-id="ea511-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="ea511-220">다음 코드에는이 작업을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="ea511-221">자세한 내용은[서비스 작업 호출 및 작업](https://msdn.microsoft.com/library/hh230677.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea511-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="ea511-222">한 가지 옵션은 확장 합니다 **컨테이너** 작업을 호출 하는 강력한 형식의 메서드를 제공 하기 위해 클래스:</span><span class="sxs-lookup"><span data-stu-id="ea511-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
