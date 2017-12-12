---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: "Web API 2.2 사용 하 여 OData v4에서 단일 만듭니다 | Microsoft Docs"
author: rick-anderson
description: "이 항목에서는 웹 API 2.2에서 OData 끝점에는 단일 항목을 정의 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 92c5056548b1e39defb28ac36f83b001dd108f5f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>단일 항목에 OData v4 Web API 2.2 사용 하 여 만들기
====================
Zoe Luo로

> 일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 OData v4 단일 및 포함, WebAPI 2.2 모두 지 원하는 두 가지 추가 옵션을 제공 합니다.


이 문서에서는 웹 API 2.2에서 OData 끝점에는 단일 항목을 정의 하는 방법을 보여 줍니다. 에 대 한 내용은 단일 무엇 이며 어떻게이 사용 하 여 얻을 수 있습니다, [특별 한 엔터티를 정의 하는 단일 항목을 사용 하 여](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)합니다. Web API에서 OData V4 끝점을 만들려면 참조 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2.2 만들](create-an-odata-v4-endpoint.md)합니다. 

에서는 다음 데이터 모델을 사용 하 여 웹 API 프로젝트에는 단일 항목을 생성 합니다.

![데이터 모델](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

명명 된 단일 `Umbrella` 유형에 따라 정의 됩니다 `Company`, 엔터티 명명 된 집합 및 `Employees` 유형에 따라 정의 됩니다 `Employee`합니다.

이 자습서에 사용 되는 솔루션에서 다운로드할 수 있습니다 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)합니다.

## <a name="define-the-data-model"></a>데이터 모델 정의

1. CLR 형식을 정의 합니다.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. CLR 유형을 기반으로 하는 EDM 모델을 생성 합니다.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    여기에서 `builder.Singleton<Company>("Umbrella")` 모델 작성기 라는 단일 만들를 지시 `Umbrella` EDM 모델에서입니다.

    생성 된 메타 데이터는 다음과 같이 표시 됩니다.

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    메타 데이터에서 볼 수 있습니다 하는 탐색 속성 `Company` 에 `Employees` 엔터티 집합은 단일 항목에 바인딩된 `Umbrella`합니다. 바인딩이 자동으로 수행 됩니다 `ODataConventionModelBuilder`, 이후만 `Umbrella` 에 `Company` 유형입니다. 사용할 수 있습니다는 모델에 모호성이 있으면 `HasSingletonBinding` 단일; 항목에 탐색 속성을 명시적으로 바인딩할 수 `HasSingletonBinding` 를 사용 하 여 것과 동일한 결과가 `Singleton` CLR 유형 정의에 특성:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>단일 컨트롤러를 정의 합니다.

EntitySet 컨트롤러 처럼 단일 컨트롤러에서 상속 `ODataController`, 단일 컨트롤러 이름은 수 및 `[singletonName]Controller`합니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

다양 한 종류의 요청을 처리 하기 위해 컨트롤러에 미리 정의 된 되도록 작업이 필요 합니다. **라우팅 특성** WebApi 2.2에는 기본적으로 사용 됩니다. 예를 들어, 쿼리를 처리 하는 동작을 정의 하려면 `Revenue` 에서 `Company` 특성 라우팅을 사용 하 여 다음을 사용 합니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

각 작업에 대 한 특성을 정의 하려면 원하지 않는 경우 다음 작업을 정의 [OData 라우팅 규칙](../odata-routing-conventions.md)합니다. 키를 쿼리 하는 단일 항목에 대 한 필요 하지 않은 있으므로 단일 컨트롤러에 정의 된 작업 entityset 컨트롤러에 정의 된 작업와에서 약간 다릅니다.

참조를 위해 단일 컨트롤러의 모든 작업 정의 대 한 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

기본적으로, 이것이 서비스 쪽에서 수행 해야 합니다. [샘플 프로젝트](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) 모든 솔루션 및 단일 항목을 사용 하는 방법을 보여 주는 OData 클라이언트에 대 한 코드를 포함 합니다. 단계를 수행 하 여 클라이언트를 빌드할 [OData v4 클라이언트 응용 프로그램을 만들](create-an-odata-v4-client-app.md)합니다.

입니다. 

*이 문서의 원본 콘텐츠에 대 한 Leo Hu을 가져주셔서 감사 합니다.*
