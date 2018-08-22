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
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Web API 2.2 사용 하 여 OData v4에서 Singleton 만들기
====================
Zoe Luo 여

> 일반적으로 엔터티는 엔터티 집합 내에서 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 OData v4 단일, 포함, WebAPI 2.2 둘 다 지원 두 개의 추가 옵션을 제공 합니다.


이 문서에서는 Web API 2.2에서 OData 끝점에는 단일 항목을 정의 하는 방법을 보여 줍니다. 어떤 단일 이며이 사용 하 여 얻을 수 있습니다 하는 방법에 대 한 내용은 참조 하세요 [특별 한 엔터티를 정의 하는 단일 항목을 사용 하 여](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)입니다. Web API에서 OData V4 끝점을 만들려면 참조 [OData v4 끝점 사용 하 여 ASP.NET Web API 2.2 만들기](create-an-odata-v4-endpoint.md)합니다. 

다음 데이터 모델을 사용 하 여 Web API 프로젝트의 단일 항목을 만듭니다.

![데이터 모델](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

라는 단일 `Umbrella` 형식에 따라 정의 됩니다 `Company`, 및 엔터티 명명 된 집합 `Employees` 종류에 따라 정의 됩니다 `Employee`합니다.

이 자습서에 사용 되는 솔루션에서 다운로드할 수 있습니다 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)합니다.

## <a name="define-the-data-model"></a>데이터 모델 정의

1. CLR 형식을 정의 합니다.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. CLR 형식을 기반으로 EDM 모델을 생성 합니다.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    이때 `builder.Singleton<Company>("Umbrella")` 라는 단일을 만들려면 모델 작성기를 알려 줍니다 `Umbrella` EDM 모델에 있습니다.

    생성된 된 메타 데이터는 다음과 같이 표시 됩니다.

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    메타 데이터에서 확인할 수 있는 탐색 속성 `Company` 에 `Employees` 엔터티 집합을 singleton 바인딩된 `Umbrella`합니다. 바인딩을 자동으로 수행 됩니다 `ODataConventionModelBuilder`, 이후만 `Umbrella` 에 `Company` 형식입니다. 사용할 수 있으면 모호성 모델에서 `HasSingletonBinding` 바인딩할 명시적으로 탐색 속성을 단일; `HasSingletonBinding` 사용 하는 것과 동일한 효과가 `Singleton` CLR 유형 정의의 특성:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>단일 컨트롤러를 정의 합니다.

EntitySet 컨트롤러와 같은 단일 컨트롤러에서 상속 `ODataController`, 단일 컨트롤러 이름 이어야 합니다 하 고 `[singletonName]Controller`입니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

다른 종류의 요청을 처리 하기 위해 컨트롤러에서 미리 정의 된 되도록 작업이 필요 합니다. **특성 라우팅** WebApi 2.2에는 기본적으로 사용 됩니다. 예를 들어 쿼리를 처리 하는 동작을 정의 하려면 `Revenue` 에서 `Company` 특성 라우팅을 사용 하 여 다음을 사용 합니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

각 작업에 대 한 특성을 정의 하려는 경우 다음 작업 정의할 [OData 라우팅 규칙](../odata-routing-conventions.md)합니다. 키가 단일 쿼리를 위한 필수 이므로 단일 컨트롤러에 정의 된 작업의 entityset 컨트롤러에 정의 된 작업에서 약간 다릅니다.

참조에 대 한 단일 컨트롤러의 모든 작업 정의 대 한 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

기본적으로 이것이 서비스 쪽에서 수행 해야 합니다. 합니다 [샘플 프로젝트](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) 모든 솔루션 및 단일 항목을 사용 하는 방법을 보여 주는 OData 클라이언트에 대 한 코드를 포함 합니다. 단계를 수행 하 여 클라이언트를 빌드할 [OData v4 클라이언트 앱을 만드는](create-an-odata-v4-client-app.md)합니다.

. 

*Leo Hu에이 문서의 원래 콘텐츠에 참여해 주셔서 감사 합니다.*
