---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2에서에서 OData 작업을 지 원하는 | Microsoft Docs
author: MikeWasson
description: 'Odata에서 작업은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 작업에 대 한 일부 사용: 구현 하는 중...'
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: 71c0f91f709aca0deb5548bdbcad60d79a2702f6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827090"
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2 OData 작업 지원
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Odata에서 *작업* 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 작업에 대 한 몇 가지 용도 다음과 같습니다.
> 
> - 복잡 한 트랜잭션을 구현 합니다.
> - 한 번에 여러 엔터티를 조작 합니다.
> - 엔터티의 특정 속성에만 업데이트를 허용합니다.
> - 엔터티의 정의 되지 않은 서버에 전송 정보입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - OData 버전 3
> - Entity Framework 6


## <a name="example-rating-a-product"></a>예: 제품 등급

이 예제에서는 사용자가 제품을 평가 하 고 각 제품에 대 한 평균 등급을 노출할 수 있도록 하려고 합니다. 데이터베이스에서 제품 키가 지정 된 등급의 목록이 저장 됩니다.

모델에서는 Entity Framework의 등급을 나타내는 데 사용할 수는 다음과 같습니다.

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

게시물에는 클라이언트에서는 싶지만 `ProductRating` "등급" 컬렉션 개체입니다. 직관적으로 등급을 제품 컬렉션을 사용 하 여 연결 되며 클라이언트에만 등급 값을 게시 해야 합니다.

따라서 일반적인 CRUD 작업을 사용 하는 대신 정의 클라이언트가 호출할 수 있는 작업 제품입니다. 작업의 OData 용어 *바인딩된* Product 엔터티를 합니다.

>작업 서버에서 의도 하지 않은 경우 이 따라서가에 대 한 HTTP POST 요청을 사용 하 여 호출 됩니다. 작업 매개 변수 및 서비스 메타 데이터에서 설명 하는 반환 형식이 있을 수 있습니다. 클라이언트 요청 본문에 매개 변수를 보내고 서버는 응답 본문에 반환 값을 보냅니다. "속도 제품" 작업을 호출 하려면 클라이언트 다음과 같은 URI에 POST를 보냅니다.

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 요청에 데이터는 제품 등급 하기만 하면 됩니다.

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>엔터티 데이터 모델에서 작업을 선언 합니다.

Web API 구성에는 EDM (엔터티 데이터 모델)에 작업을 추가 합니다.

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

이 코드는 제품 엔터티에 대해 수행할 수 있는 작업으로 "RateProduct"를 정의 합니다. 작업을 사용 한다고 선언도 **int** 매개 변수 "등급" 라는 및 반환는 **int** 값입니다.

## <a name="add-the-action-to-the-controller"></a>컨트롤러에 작업 추가

"RateProduct" 작업을 제품 엔터티에 바인딩됩니다. 작업을 구현 하려면 라는 메서드를 추가 `RateProduct` 제품 컨트롤러:

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

메서드 이름은 EDM에서 작업의 이름과 일치 하는지 확인 합니다. 메서드가 두 개의 매개 변수:

- *키*: 속도에 제품에 대 한 키입니다.
- *매개 변수*: 작업 매개 변수 값의 사전입니다.

기본 라우팅 규칙을 사용 하는 경우 키 매개 변수 이름은 "키"입니다. 포함 하는 일을 해야 이기도 합니다 **[FromOdataUri]** 특성으로 표시 된 것 처럼 합니다. 이 특성은 요청 URI에서에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하는 웹 API에 알립니다.

사용 된 *매개 변수* 사전 작업 매개 변수를 가져오려면:

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

클라이언트에서 올바른 작업 매개 변수를 보내는 경우, 값의 형식을 **ModelState.IsValid** 그렇습니다. 이 경우 사용할 수 있습니다 합니다 **ODataActionParameters** 사전 매개 변수 값을 가져옵니다. 이 예제는 `RateProduct` "등급" 라는 단일 매개 변수를 사용 하는 작업입니다.

## <a name="action-metadata"></a>작업 메타 데이터

서비스 메타 데이터를 보려면 /odata/$ 메타 데이터는 GET 요청을 보냅니다. 선언 하는 메타 데이터의 부분은 여기는 `RateProduct` 작업:

[!code-xml[Main](odata-actions/samples/sample7.xml)]

합니다 **FunctionImport** 요소 작업을 선언 합니다. 대부분의 필드 이름 자체로 설명 되지만 두 가지 짚고 넘어가야 할:

- **Isbindable 인** 작업 대상 엔터티를 하나 이상 호출할 수 있습니다 의미의 일부입니다.
- **IsAlwaysBindable** 작업 대상 엔터티 항상 호출할 수 있습니다 의미 합니다.

점은 일부 작업은 항상 클라이언트에 사용할 수 있지만 다른 작업의 엔터티 상태에 따라 달라질 수 있습니다. 예를 들어, "Purchase" 작업을 정의 합니다. 만 재고에 있는 항목을 구매할 수 있습니다. 항목 재고가 이면 클라이언트는 작업을 호출할 수 없습니다.

EDM을 정의 하는 경우는 **동작** 메서드는 항상 바인딩 가능 작업을 만듭니다.

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

Not-항상-바인딩할 수 있는 작업에 대 한 하겠습니다 (라고도 *일시적인* 작업)이이 항목의에서 뒷부분에 있습니다.

## <a name="invoking-the-action"></a>작업 호출

이제 클라이언트는이 작업을 호출 하는 방법을 확인해 보겠습니다. 클라이언트 ID 사용 하 여 제품에 2의 등급을 제공 하려는 가정 = 4. JSON 형식을 사용 하 여 요청 본문에 대 한 예제 요청 메시지에는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample9.cmd)]

응답 메시지는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>작업 엔터티 집합에 바인딩

이전 예제에서는 작업을 단일 엔터티에 바인딩되어: 클라이언트 단일 제품 등급을 지정 합니다. 엔터티 컬렉션에 작업을 바인딩할 수 있습니다. 다음 변경 내용을 확인 합니다.

Edm에서는 작업에 추가할 엔터티의 **컬렉션** 속성입니다.

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

컨트롤러 메서드에서 생략 합니다 *키* 매개 변수입니다.

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

이제 클라이언트는 Products 엔터티 집합에 대 한 동작을 호출합니다.

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>컬렉션 매개 변수를 사용 하 여 작업

작업에는 값의 컬렉션을 사용 하는 매개 변수가 있을 수 있습니다. EDM에서 사용 하 여 **CollectionParameter&lt;T&gt;**  매개 변수를 선언 합니다.

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

이 컬렉션을 사용 하는 "등급" 라는 매개 변수를 선언 **int** 값입니다. 컨트롤러 메서드에서 여전히 표시에서 매개 변수 값을 **ODataActionParameters** 개체가 아니라 이제 값은는 **ICollection&lt;int&gt;**  값:

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>임시 작업

"RateProduct" 예제에서는 사용자가 항상 평가할 수 제품을 작업은 항상 사용할 수 있습니다. 하지만 일부 작업의 엔터티 상태에 따라 달라 집니다. 예를 들어 비디오 차량 대 여 서비스에서 "체크 아웃" 작업을 항상 사용할 수 없는 경우 (종속 비디오의 복사를 사용할 수 있는지 됩니다.) 이 유형의 작업 호출 되는 *일시적인* 작업 합니다.

임시 작업에 서비스 메타 데이터 **IsAlwaysBindable** 같으면 false입니다. 이므로 실제로 기본값인 메타 데이터는 다음과 같이 표시 됩니다.

[!code-xml[Main](odata-actions/samples/sample16.xml)]

여기가 중요 한 이유: 서버 작업을 사용할 수 있는 경우 클라이언트에 게 알리는 해야 액션 일시적인 경우. 엔터티에서 작업에 대 한 링크를 포함 하 여 수행 합니다. 영화 엔터티에 대 한 예는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" 속성은 체크 아웃 작업에 대 한 링크를 포함 합니다. 작업에 사용할 수 없는 경우 서버는 링크를 생략 합니다.

EDM에서 일시적인 작업을 선언 하려면 호출을 **TransientAction** 메서드:

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

또한 지정 된 엔터티에 대 한 작업 링크를 반환 하는 함수를 제공 해야 합니다. 이 함수를 호출 하 여 설정할 **HasActionLink**합니다. 람다 식으로 함수를 작성할 수 있습니다.

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

작업을 사용할 수 있는 경우 람다 식을 작업에는 링크를 반환 합니다. 엔터티를 serialize 할 때이 링크를 포함 하는 OData 직렬 변환기입니다. 함수를 반환 하는 작업을 사용할 수 없을 때 `null`합니다.

## <a name="additional-resources"></a>추가 리소스

[OData 작업 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
