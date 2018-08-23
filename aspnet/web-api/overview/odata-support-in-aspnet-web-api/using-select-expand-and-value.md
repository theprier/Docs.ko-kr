---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: $Expand $select 사용 및 ASP.NET Web API 2 OData의 $value | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/11/2013
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: d198ecf40155cba36204bc0810f4735aae6b100b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837612"
---
<a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a>$Expand $select 사용 및 ASP.NET Web API 2 OData의 $value
====================
[Mike Wasson](https://github.com/MikeWasson)

Web API 2 odata에서 $value 옵션과 $select, $expand에 대 한 지원을 추가 합니다. 이러한 옵션에는 서버에서 반환 되는 표현을 제어에 대 한 클라이언트를 수 있습니다.

- **$expand** 관련 엔터티가 응답에 인라인으로 포함된 됩니다.
- **$select** 응답에 포함 될 속성의 하위 집합을 선택 합니다.
- **$value** 속성의 원시 값을 가져옵니다.

## <a name="example-schema"></a>예제 스키마

이 문서에서는 세 가지 엔터티를 정의 하는 OData 서비스를 사용 하겠습니다: 제품, 공급자 및 범주입니다. 각 제품에는 하나의 범주 및 공급자가 있습니다.

![](using-select-expand-and-value/_static/image1.png)

엔터티 모델을 정의 하는 C# 클래스는 다음과 같습니다.

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

있음을 합니다 `Product` 클래스에 대 한 탐색 속성을 정의 합니다 `Supplier` 및 `Category`합니다. `Category` 클래스 각 범주의 제품에 대 한 탐색 속성을 정의 합니다.

이 스키마에 대 한 OData 끝점을 만들려면 사용 하 여 Visual Studio 2013 스 캐 폴딩에 설명 된 대로 [ASP.NET Web API에서 OData 끝점을 만드는](odata-v3/creating-an-odata-endpoint.md)합니다. 제품, 범주 및 공급자에 대 한 별도 컨트롤러를 추가 합니다.

## <a name="enabling-expand-and-select"></a>확장 하 고 $를 사용 하도록 설정 하 고 $select

Visual Studio 2013에서 Web API OData 스 캐 폴딩을 $select 및 $expand 하는 지원 자동으로 해당 컨트롤러를 만듭니다. 참조용으로 다음은 $ 지원 요구 사항을 확장 하 고 컨트롤러에서 $select 합니다.

컬렉션의 경우 컨트롤러의 `Get` 메서드를 반환 해야 합니다는 **IQueryable**합니다.

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

단일 엔터티에 대 한 반환을 **SingleResult&lt;T&gt;**, 여기서 T는는 **IQueryable** 0 개 이상의 엔터티를 포함 하는 합니다.

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

또한 데코 레이트 하 `Get` 메서드를 **[Queryable]** 특성을 이전 코드 조각에 나와 있는 것 처럼. 또는 호출 **EnableQuerySupport** 에 **HttpConfiguration** 시작 개체입니다. (자세한 내용은 [OData 쿼리 옵션 사용](supporting-odata-query-options.md#enable).)

## <a name="using-expand"></a>$를 사용 하 여 확장

OData 엔터티 또는 컬렉션을 쿼리 하는 경우 기본 응답 관련된 엔터티를 포함 하지 않습니다. 예를 들어, 다음은 범주 엔터티 집합에 대 한 기본 응답이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

알 수 있듯이 범주 엔터티에 제품 탐색 링크를 포함 하는 경우에 응답 모든 제품을 포함 하지 않습니다. 클라이언트가 $를 사용할 수 있지만 각 범주에 대 한 제품의 목록을 가져오려면 확장 합니다. $Expand 옵션 요청의 쿼리 문자열에 이동 합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

이제 서버 제품을 각 범주에 범주를 사용 하 여 인라인 포함 됩니다. 응답 페이로드는 다음과 같습니다.

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

제품 목록 "값" 배열의 각 항목에 포함 되어 있는지 확인 합니다.

$ Expand 옵션은 쉼표로 구분 된 목록을 확장 하는 탐색 속성입니다. 다음 요청 범주 및 제품 공급 업체 확장합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

다음은 응답 본문이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

탐색 속성의 둘 이상의 수준으로 확장할 수 있습니다. 다음 예제를 범주에 대 한 모든 제품 및 각 제품의 공급 업체를 포함 합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

다음은 응답 본문이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

기본적으로 Web API 2로 최대 확장 깊이 제한합니다. 같은 복잡 한 요청을 보낸 클라이언트에 맞지 않는 `$expand=Orders/OrderDetails/Product/Supplier/Region`, 큰 응답을 만들고 쿼리를 효율적으로 수 있음. 기본값을 재정의 하려면 설정 합니다 **MaxExpansionDepth** 속성에는 **[Queryable]** 특성입니다.

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

$에 대 한 자세한 내용은 expand 옵션을 참조 하세요 [확장 System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) 공식 OData 설명서에서.

## <a name="using-select"></a>$Select을 사용 하 여

$Select 옵션은 응답 본문에 포함 될 속성의 하위 집합을 지정 합니다. 예를 들어, 이름 및 각 제품의 가격을 가져오려면 다음 쿼리를 사용 합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

다음은 응답 본문이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

$Select 결합할 수 있습니다 하 고 동일한 쿼리에 $expand입니다. $Select 옵션에서 확장된 된 속성을 포함 해야 합니다. 예를 들어 다음 요청은 제품 이름 및 공급자를 가져옵니다.

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

다음은 응답 본문이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

또한 확장된 된 속성에서 속성을 선택할 수 있습니다. 다음 요청 제품을 확장 하 고 범주 이름과 제품 이름을 선택 합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

다음은 응답 본문이입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

$Select 옵션에 대 한 자세한 내용은 참조 하세요. [Select 시스템 쿼리 옵션 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) 공식 OData 설명서에서.

## <a name="getting-individual-properties-of-an-entity-value"></a>엔터티 ($value)의 개별 속성 가져오기

두 가지 방법으로 OData 클라이언트 엔터티의 개별 속성을 가져오려고 합니다. 클라이언트를 OData 형식으로 값을 다운로드 하거나 속성의 원시 값을 가져올 수 있습니다.

다음 요청을 OData 형식에서 속성을 가져옵니다.

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

다음은 JSON 형식으로 응답 예제입니다.

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

속성의 원시 값을 검색할 $value URI에 추가 합니다.

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

응답은 다음과 같습니다. 콘텐츠 형식이 "text/plain" 하지 JSON 알 수 있습니다.

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

OData 컨트롤러에서 이러한 쿼리를 지원 하려면 라는 메서드를 추가 `GetProperty`여기서 `Property` 속성의 이름입니다. Name 속성을 가져올 메서드의 이름이 예를 들어 `GetName`합니다. 메서드는 해당 속성의 값을 반환 해야 합니다.

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
