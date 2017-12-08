---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: "ASP.NET Web API 2 OData 작업을 지 원하는 | Microsoft Docs"
author: MikeWasson
description: "Odata에서 작업은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 작업에 대 한 일부 사용: 구현 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: acb369ca8f1bab8d7cad14c15f46cfd44beb9fdd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2 OData 작업을 지 원하는
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Odata에서 *동작* 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 작업에 대 한 몇 가지 팁은 다음과 같습니다.
> 
> - 복잡 한 트랜잭션에 구현 합니다.
> - 한 번에 몇 개의 엔터티를 조작 합니다.
> - 엔터티의 특정 속성에만 업데이트를 허용 합니다.
> - 엔터티의 정의 되지 않은 서버에 정보를 보냅니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - OData 버전 3
> - Entity Framework 6


## <a name="example-rating-a-product"></a>예: 제품 평가

이 예제에서는 사용자가 제품을 평가 하 고 그런 다음 각 제품에 대 한 평균 등급을 제공 하려고 합니다. 다음은 데이터베이스에서의 등급, 제품 키가 지정 된 목록을 저장 됩니다.

다음은 Entity Framework의 등급을 나타내기 위해 사용할 것 모델이입니다.

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

클라이언트가 POST 않도록 하지만 `ProductRating` "등급" 컬렉션 개체를 합니다. 직관적으로 등급 제품 컬렉션에 연결 되며 클라이언트 해야 등급 값을 게시 합니다.

따라서 기본 CRUD 작업을 사용 하는 대신 정의 클라이언트가 호출할 수 있는 동작 제품. 작업은 OData 용어로 *바인딩된* 제품 엔터티.

>부작용에 서버에 있어야 하는 작업입니다. 이러한 이유로 HTTP POST 요청을 사용 하 여 호출 됩니다. 작업 매개 변수 및 서비스 메타 데이터에서 설명 하는 반환 형식을 가질 수 있습니다. 클라이언트 요청 본문에는 매개 변수 보내고 서버 응답 본문에 반환 값을 보냅니다. "속도 제품" 작업을 호출 하려면 클라이언트 다음과 같은 URI에 POST를 보냅니다.

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 요청에 대 한 데이터는 단순히 제품 등급:

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>엔터티 데이터 모델의 작업을 선언

Web API 구성에서는 엔터티 데이터 모델 (EDM)에 동작을 추가 합니다.

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

이 코드는 "RateProduct" 제품 엔터티에 대해 수행할 수 있는 동작으로 정의 합니다. 또한 동작이 선언는 **int** "등급" 라는 하 고 반환 하는 매개 변수는 **int** 값입니다.

## <a name="add-the-action-to-the-controller"></a>컨트롤러에 추가 하는 작업

"RateProduct" 동작을 제품 엔터티에 바인딩되어 있습니다. 라는 메서드를 추가 동작을 구현 하려면 `RateProduct` 제품 컨트롤러에:

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

메서드 이름이 EDM의 동작의 이름과 일치 하는지 확인 합니다. 메서드에 두 개의 매개 변수가 있습니다.

- *키*: 등급을 제품에 대 한 키입니다.
- *매개 변수*: 작업 매개 변수 값의 사전입니다.

기본 라우팅 규칙을 사용 하는 키 매개 변수 이름을 지정 해야 "키"입니다. 포함 하는 것이 중요 이기도 **[FromOdataUri]** 특성으로 표시 된 것 처럼 합니다. 이 특성은 요청 URI에서에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하도록 Web API를 알려 줍니다.

사용 하 여는 *매개 변수* 사전 작업 매개 변수를 가져오려면:

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

클라이언트에서 올바른 작업 매개 변수를 보내는 경우, 값의 서식을 **ModelState.IsValid** 그렇습니다. 이 경우 사용할 수 있습니다는 **ODataActionParameters** 사전 매개 변수 값을 가져옵니다. 이 예제는 `RateProduct` "등급" 라는 단일 매개 변수를 사용 하는 작업입니다.

## <a name="action-metadata"></a>동작 메타 데이터

서비스 메타 데이터를 보려면 /odata/$ 메타 데이터에 GET 요청을 보냅니다. 선언 하는 메타 데이터의 부분입니다. 여기에서 `RateProduct` 동작:

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport** 요소 작업을 선언 합니다. 대부분의 필드 이름 자체로 설명 되지만 두 가지 주요 데이터:

- **Isbindable 인** 는 동작을 호출할 수 대상 엔터티의 이상 의미 일정 시간입니다.
- **IsAlwaysBindable** 동작을 호출 하 여 대상 엔터티의 항상 수를 의미 합니다.

차이가 일부 작업은 항상 클라이언트를 사용할 수 있지만 다른 작업의 엔터티 상태에 따라 달라질 수 있습니다. 예를 들어, "Purchase" 동작을 정의 합니다. 만 재고에 있는 항목을 구입할 수 있습니다. 항목이 out of stock 경우 클라이언트가 해당 동작을 호출할 수 없습니다.

EDM에 정의 하는 경우는 **동작** 메서드는 항상 바인딩 가능 작업을 만듭니다.

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

Not 항상-바인딩 가능한 동작에 대 한 하겠습니다 (호출 또한 *일시적인* 작업)이이 항목의 뒷부분에 나오는 합니다.

## <a name="invoking-the-action"></a>다음 작업을 호출

이제 클라이언트는이 작업을 호출 하는 방법을 알아봅니다. 클라이언트 ID 인 제품에 2의 등급을 제공 하려는 경우를 가정해 볼 = 4. 다음은 JSON 형식을 사용 하 여 요청 본문에 대 한 예제 요청 메시지가입니다.

[!code-console[Main](odata-actions/samples/sample9.cmd)]

응답 메시지는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>작업 엔터티 집합에 바인딩

이전 예에서 동작이 단일 엔터티에 바인딩된: 클라이언트 단일 제품의 등급을 지정 합니다. 또한 엔터티를 컬렉션에 작업을 바인딩할 수 있습니다. 단지 다음과 같이 변경을 합니다.

Edm에서는 동작 엔터티의을 추가 **컬렉션** 속성입니다.

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

컨트롤러 메서드의 생략는 *키* 매개 변수입니다.

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

이제 클라이언트 제품 엔터티 집합에 대해 작업을 호출 합니다.

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>컬렉션 매개 변수를 사용 하 여 작업

작업 값의 컬렉션을 사용 하는 매개 변수를 가질 수 있습니다. EDM에서 사용 하 여 **CollectionParameter&lt;T&gt;**  를 매개 변수를 선언 합니다.

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

컬렉션을 사용 하는 "등급" 라는 매개 변수를 선언 하는이 **int** 값입니다. 컨트롤러 메서드를 여전히 매개 변수 값을가 가져올는 **ODataActionParameters** 개체가 아니라 이제 값은 한 **ICollection&lt;int&gt;**  값:

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>임시 작업

"RateProduct" 예제에서는 사용자가 항상 평가할 수, 제품 동작은 항상 사용할 수 있도록. 하지만 일부 작업의 엔터티 상태에 따라 다릅니다. 예를 들어, 비디오 대 여 서비스에서 "체크 아웃" 작업 항상 사용할 수 없는 경우 (종속 해당 비디오의 복사본은 사용할 수 있는지 여부를.) 이러한 종류의 동작은 라고는 *일시적인* 동작 합니다.

일시적인 동작에 서비스 메타 데이터를 **IsAlwaysBindable** false 같음. 이므로 실제로 기본 값, 메타 데이터는 다음과 같습니다.

[!code-xml[Main](odata-actions/samples/sample16.xml)]

여기가 중요 한 이유: 서버가 동작은 사용할 수 있는 클라이언트에 게 알리는 해야 일시적인 작업의 경우. 엔터티에서 작업에 대 한 링크를 포함 하 여 수행 합니다. 영화 엔터티에 대 한 예는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" 속성은 체크 아웃 작업에 대 한 링크를 포함 합니다. 서버 작업에 사용할 수 없는 경우 링크를 생략 합니다.

EDM의 임시 작업을 선언 하려면 호출는 **TransientAction** 메서드:

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

또한 특정된 엔터티에 대 한 작업 링크를 반환 하는 함수를 제공 해야 합니다. 이 함수를 호출 하 여 설정 **HasActionLink**합니다. 람다 식으로 함수를 작성할 수 있습니다.

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

작업이 사용할 수 있는 경우 람다 식을 작업에 대 한 링크를 반환 합니다. 엔터티를 serialize 할 때이 링크를 포함 하는 OData 직렬 변환기입니다. 함수를 반환 하는 작업에 사용할 수 없는 경우 `null`합니다.

## <a name="additional-resources"></a>추가 리소스

[OData 작업 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
