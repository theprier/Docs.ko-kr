---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2.2 사용 하 여 OData v4에서 Singleton 만들기 | Microsoft Docs
author: rick-anderson
description: 이 항목에서는 Web API 2.2에서 OData 끝점에는 단일 항목을 정의 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 7562a90ae34b216dca2dd3cf541d086585735212
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831877"
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="83500-103">Web API 2.2 사용 하 여 OData v4에서 Singleton 만들기</span><span class="sxs-lookup"><span data-stu-id="83500-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>
====================
<span data-ttu-id="83500-104">Zoe Luo 여</span><span class="sxs-lookup"><span data-stu-id="83500-104">by Zoe Luo</span></span>

> <span data-ttu-id="83500-105">일반적으로 엔터티는 엔터티 집합 내에서 캡슐화 된 경우에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83500-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="83500-106">하지만 OData v4 단일, 포함, WebAPI 2.2 둘 다 지원 두 개의 추가 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="83500-107">이 문서에서는 Web API 2.2에서 OData 끝점에는 단일 항목을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83500-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="83500-108">어떤 단일 이며이 사용 하 여 얻을 수 있습니다 하는 방법에 대 한 내용은 참조 하세요 [특별 한 엔터티를 정의 하는 단일 항목을 사용 하 여](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="83500-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="83500-109">Web API에서 OData V4 끝점을 만들려면 참조 [OData v4 끝점 사용 하 여 ASP.NET Web API 2.2 만들기](create-an-odata-v4-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="83500-110">다음 데이터 모델을 사용 하 여 Web API 프로젝트의 단일 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83500-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![데이터 모델](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="83500-112">라는 단일 `Umbrella` 형식에 따라 정의 됩니다 `Company`, 및 엔터티 명명 된 집합 `Employees` 종류에 따라 정의 됩니다 `Employee`합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="83500-113">이 자습서에 사용 되는 솔루션에서 다운로드할 수 있습니다 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="83500-114">데이터 모델 정의</span><span class="sxs-lookup"><span data-stu-id="83500-114">Define the data model</span></span>

1. <span data-ttu-id="83500-115">CLR 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="83500-116">CLR 형식을 기반으로 EDM 모델을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="83500-117">이때 `builder.Singleton<Company>("Umbrella")` 라는 단일을 만들려면 모델 작성기를 알려 줍니다 `Umbrella` EDM 모델에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83500-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="83500-118">생성된 된 메타 데이터는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83500-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="83500-119">메타 데이터에서 확인할 수 있는 탐색 속성 `Company` 에 `Employees` 엔터티 집합을 singleton 바인딩된 `Umbrella`합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="83500-120">바인딩을 자동으로 수행 됩니다 `ODataConventionModelBuilder`, 이후만 `Umbrella` 에 `Company` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="83500-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="83500-121">사용할 수 있으면 모호성 모델에서 `HasSingletonBinding` 바인딩할 명시적으로 탐색 속성을 단일; `HasSingletonBinding` 사용 하는 것과 동일한 효과가 `Singleton` CLR 유형 정의의 특성:</span><span class="sxs-lookup"><span data-stu-id="83500-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="83500-122">단일 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-122">Define the singleton controller</span></span>

<span data-ttu-id="83500-123">EntitySet 컨트롤러와 같은 단일 컨트롤러에서 상속 `ODataController`, 단일 컨트롤러 이름 이어야 합니다 하 고 `[singletonName]Controller`입니다.</span><span class="sxs-lookup"><span data-stu-id="83500-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="83500-124">다른 종류의 요청을 처리 하기 위해 컨트롤러에서 미리 정의 된 되도록 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="83500-125">**특성 라우팅** WebApi 2.2에는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83500-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="83500-126">예를 들어 쿼리를 처리 하는 동작을 정의 하려면 `Revenue` 에서 `Company` 특성 라우팅을 사용 하 여 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="83500-127">각 작업에 대 한 특성을 정의 하려는 경우 다음 작업 정의할 [OData 라우팅 규칙](../odata-routing-conventions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="83500-128">키가 단일 쿼리를 위한 필수 이므로 단일 컨트롤러에 정의 된 작업의 entityset 컨트롤러에 정의 된 작업에서 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="83500-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="83500-129">참조에 대 한 단일 컨트롤러의 모든 작업 정의 대 한 메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83500-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="83500-130">기본적으로 이것이 서비스 쪽에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="83500-131">합니다 [샘플 프로젝트](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) 모든 솔루션 및 단일 항목을 사용 하는 방법을 보여 주는 OData 클라이언트에 대 한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="83500-132">단계를 수행 하 여 클라이언트를 빌드할 [OData v4 클라이언트 앱을 만드는](create-an-odata-v4-client-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83500-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="83500-133">.</span><span class="sxs-lookup"><span data-stu-id="83500-133">.</span></span> 

<span data-ttu-id="83500-134">*Leo Hu에이 문서의 원래 콘텐츠에 참여해 주셔서 감사 합니다.*</span><span class="sxs-lookup"><span data-stu-id="83500-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
