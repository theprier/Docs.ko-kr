---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: "Web API 2.2 사용 하 여 OData v4에 포함 | Microsoft Docs"
author: rick-anderson
description: "일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 단일 및 Con 두 개의 추가 옵션을 제공 하는 OData v4..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 7d3c81bf3d2a43faa3e71155637e031f81143782
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2.2 사용 하 여 OData v4에 포함
====================
Jinfu Tan으로

> 일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 OData v4 단일 및 포함, WebAPI 2.2 모두 지 원하는 두 가지 추가 옵션을 제공 합니다.


이 항목에서는 WebApi 2.2에서 OData 끝점에는 포함을 정의 하는 방법을 보여 줍니다. 포함 하는 방법에 대 한 자세한 내용은 참조 [제약 OData v 4와 예정 사항](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)합니다. Web API에서 OData V4 끝점을 만들려면 참조 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2.2 만들](create-an-odata-v4-endpoint.md)합니다.

첫째, 만들겠습니다 포함 도메인 모델에 있는 OData 서비스에서이 데이터 모델을 사용 하 여:

![데이터 모델](odata-containment-in-web-api-22/_static/image1.png)

계정을 많은 PaymentInstruments (PI)를 포함 하지만 엔터티는 PI에 대 한 집합을 정의 하지 않습니다. 대신,는 Pi 계정을 통해 액세스할 수만 있습니다.

이 항목에 사용 되는 솔루션을 다운로드할 수 있습니다 [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)합니다.

## <a name="defining-the-data-model"></a>데이터 모델 정의

1. CLR 형식을 정의 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained` 특성 포함 탐색 속성에 사용 됩니다.
2. CLR 유형을 기반으로 하는 EDM 모델을 생성 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder` EDM 모델을 작성 하는 경우를 처리 하는 `Contained` 특성이 해당 탐색 속성에 추가 됩니다. 속성 컬렉션 형식이 면는 `GetCount(string NameContains)` 함수도 생성 됩니다.

    생성 된 메타 데이터는 다음과 같이 표시 됩니다.

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget` 특성 탐색 속성이 포함 인지를 나타냅니다.

## <a name="define-the-containing-entity-set-controller"></a>포함 된 엔터티 집합 컨트롤러를 정의 합니다.

포함 된 엔터티 자체 컨트롤러; 없는 합니다. 작업은 포함 하는 엔터티 집합 컨트롤러에 정의 됩니다. 이 샘플은 됩니다는 AccountsController PaymentInstrumentsController 없습니다.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData 경로 세그먼트를 4 개 이상 있으면만 라우팅의 작동 같은 특성 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 위의 컨트롤러에 있습니다. 특성 및 규칙에 따른 라우팅 모두 작동 하는 그렇지 않은 경우: 예를 들어, `GetPayInPIs(int key)` 일치 `GET ~/Accounts(1)/PayinPIs`합니다.

*이 문서의 원본 콘텐츠에 대 한 Leo Hu을 가져주셔서 감사 합니다.*
