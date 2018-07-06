---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2.2 사용 하 여 OData v4의 제약 | Microsoft Docs
author: rick-anderson
description: 일반적으로 엔터티는 엔터티 집합 내에서 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 OData v4 Singleton 및 Con 두 개의 추가 옵션을 제공 하는 중...
ms.author: aspnetcontent
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 56e550b56e9ad237dbf4fab04f2bd545164ee90a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824914"
---
<a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2.2 사용 하 여 OData v4의 제약
====================
Jinfu Tan 여

> 일반적으로 엔터티는 엔터티 집합 내에서 캡슐화 된 경우에 액세스할 수 없습니다. 하지만 OData v4 단일, 포함, WebAPI 2.2 둘 다 지원 두 개의 추가 옵션을 제공 합니다.


이 항목에서는 WebApi 2.2에서 OData 끝점의 제약을 정의 하는 방법을 보여 줍니다. 포함 하는 방법에 대 한 자세한 내용은 참조 하세요. [포함 제공 되는 OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)합니다. Web API에서 OData V4 끝점을 만들려면 참조 [OData v4 끝점 사용 하 여 ASP.NET Web API 2.2 만들기](create-an-odata-v4-endpoint.md)합니다.

첫째, 만듭니다 포함 도메인 모델 OData 서비스에서이 데이터 모델을 사용 하 여:

![데이터 모델](odata-containment-in-web-api-22/_static/image1.png)

계정이 여러 PaymentInstruments (PI)를 포함 하지만 엔터티를 PI에 대 한 집합을 정의 하지 않습니다. 대신, Pi 계정을 통해 액세스할 수만 있습니다.

이 항목에 사용 되는 솔루션을 다운로드할 수 있습니다 [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)합니다.

## <a name="defining-the-data-model"></a>데이터 모델 정의

1. CLR 형식을 정의 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained` 특성 포함 탐색 속성에 사용 됩니다.
2. CLR 형식을 기반으로 EDM 모델을 생성 합니다.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    합니다 `ODataConventionModelBuilder` 경우 EDM 모델을 작성 하는 데 처리할는 `Contained` 특성이 해당 탐색 속성에 추가 됩니다. 속성 컬렉션 형식인 경우는 `GetCount(string NameContains)` 함수도 생성 됩니다.

    생성된 된 메타 데이터는 다음과 같이 표시 됩니다.

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget` 특성 임을 탐색 속성을 포함 합니다.

## <a name="define-the-containing-entity-set-controller"></a>포함 된 엔터티 집합 컨트롤러 정의

포함 된 엔터티 자체 컨트롤러가 없는 합니다. 작업을 포함 하는 엔터티 집합 컨트롤러에서 정의 됩니다. 이 샘플에서는 됩니다는 AccountsController PaymentInstrumentsController 없습니다.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData 경로 세그먼트 4 이상의 경우만 특성 라우팅의 작동과 같은 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 위의 컨트롤러에 있습니다. 특성 및 규칙 기반 라우팅 작동 하는 고, 그렇지: 예를 들어 `GetPayInPIs(int key)` 일치 `GET ~/Accounts(1)/PayinPIs`합니다.

*Leo Hu에이 문서의 원래 콘텐츠에 참여해 주셔서 감사 합니다.*
