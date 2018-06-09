---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4 에서도 | Microsoft Docs
author: MikeWasson
description: OData, 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 532362f0c0faaaf0cb0c04726856f0497e5261b5
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508232"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4에 함수
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> OData, 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 웹 API 2.2를 사용 하 여 OData v4 끝점에 동작 및 기능을 추가 하는 방법을 보여 줍니다. 이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들기](create-an-odata-v4-endpoint.md)
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2.2
> - OData v4
> - [Visual Studio 2013 업데이트 2](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - .NET 4.5
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> OData 버전 3에 대 한 참조 [ASP.NET Web API 2에서 OData 작업](../odata-v3/odata-actions.md)합니다.


차이 *동작* 및 *함수* 의도 하지 않은 작업 수 고 함수는 그렇지 않습니다. 동작과 함수는 데이터를 반환할 수 있습니다. 작업에 대 한 몇 가지 팁은 다음과 같습니다.

- 복잡 한 트랜잭션에 합니다.
- 한 번에 몇 개의 엔터티를 조작 합니다.
- 엔터티의 특정 속성에만 업데이트를 허용 합니다.
- 엔터티를 하지 않은 데이터를 보내는 중입니다.

함수는 엔터티 또는 컬렉션에 직접 해당 하지 않는 정보를 반환 하는 데 유용 합니다.

작업 (또는 함수) 대상으로 지정할 수 하나의 엔터티 또는 컬렉션입니다. 이 OData 용어에서는 *바인딩*합니다. 할 수도 있습니다 &quot;언바운드&quot; 작업/함수, 서비스에서 정적 작업으로 호출 합니다.

## <a name="example-adding-an-action"></a>예: 작업 추가

제품 평가 하는 작업을 정의 해보겠습니다.

> [!NOTE]
> 이 자습서를 기반으로 한이 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들기](create-an-odata-v4-endpoint.md)


먼저 추가 하는 `ProductRating` 등급을 나타내기 위해 모델입니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

또한 추가 **DbSet** 에 `ProductsContext` 클래스를 데이터베이스의 EF는 등급 테이블을 만듭니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>EDM에 작업 추가

WebApiConfig.cs, 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**EntityTypeConfiguration.Action** 메서드 (EDM)의 엔터티 데이터 모델에 작업을 추가 합니다. **매개 변수** 메서드 동작에 대해 입력된 된 매개 변수를 지정 합니다.

또한이 코드는 EDM에 대 한 네임 스페이스를 설정합니다. 네임 스페이스 작업에 대 한 URI 동작 정규화 된 이름을 포함 하기 때문에 적용 됩니다.

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 일반적인 IIS 구성에서이 URL에서 점을 404 오류를 반환 하도록 IIS를 발생 합니다. 다음 섹션을 Web.Config 파일에 추가 하 여이 해결할 수 있습니다.

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>작업에 대 한 컨트롤러 메서드를 추가 합니다.

사용할 수 있도록는 &quot;속도&quot; 동작을 추가 하기 위해 다음 메서드 `ProductsController`:

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

메서드 이름이 작업 이름과 일치 하는지 확인 합니다. **[HttpPost]** HTTP POST 메서드는 특성을 지정 합니다.

클라이언트는 작업을 호출 하려면 다음과 같은 HTTP POST 요청을 보냅니다.

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

&quot;속도&quot; 동작이 제품 인스턴스를 바인딩된 작업에 대 한 URI 엔터티 URI에 추가 하는 정식 동작 이름입니다. (EDM 네임 스페이스 설정 했으므로 회수 &quot;ProductService&quot;동작 정규화 된 이름이 표시 됩니다, &quot;ProductService.Rate&quot;.)

요청 본문 JSON 페이로드로 작업 매개 변수를 포함합니다. Web API에 JSON 페이로드를 자동으로 변환 된 **ODataActionParameters** 개체 매개 변수 값의 사전 뿐입니다. 이 사전을 사용 하 여 컨트롤러 메서드의 매개 변수를 액세스할 수 있습니다.

클라이언트에서 잘못 된 작업 매개 변수를 보내는 경우, 값의 서식을 **ModelState.IsValid** 은 false입니다. 컨트롤러 메서드의이 플래그를 확인 하 고 오류가 반환 **IsValid** 은 false입니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>예: 함수 추가

이제 가장 비용이 많이 드는 제품을 반환 하는 OData 함수를 추가 해 보겠습니다. 로 이전에 첫 번째 단계는 함수를 추가 EDM입니다. WebApiConfig.cs, 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

이 경우 함수는 개별 제품 인스턴스가 아닌 제품 컬렉션에 바인딩되어 있습니다. GET 요청을 전송 하 여 함수를 호출 하는 클라이언트:

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

메서드 이름이 함수 이름과 일치 하는지 확인 합니다. **[HttpGet]** HTTP GET이 메서드는 특성을 지정 합니다.

HTTP 응답은 다음과 같습니다.

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>예: 추가 언바운드 함수

앞의 예제 작업은 컬렉션에 바인딩된 기능입니다. 다음 예제에서는 만들어는 *바인딩되지 않은* 함수입니다. 바인딩되지 않은 함수는 정적 서비스 작업으로 호출 됩니다. 이 예제 함수는 지정된 된 우편 번호에 대 한 판매 세금을 반환 합니다.

경우 WebApiConfig 파일에서 EDM에 함수를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

호출 하는 **함수** 에서 직접는 **된**, 엔터티 형식 또는 컬렉션을 대신 합니다. 함수는 바인딩된 모델 작성기 지시 합니다.

함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

이 메서드를 배치 하는 Web API 컨트롤러는 중요 하지 않습니다. 빠뜨릴 수 `ProductsController`, 하거나 별도 컨트롤러를 정의 합니다. **[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.

다음은 예제 클라이언트 요청이입니다.

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 응답:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
