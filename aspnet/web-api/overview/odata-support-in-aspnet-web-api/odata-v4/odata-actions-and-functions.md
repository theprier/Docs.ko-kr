---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 동작 및 ASP.NET Web API 2.2 사용 하 여 OData v4의 기능 | Microsoft Docs
author: MikeWasson
description: OData에서 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 방법...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 4e61c6b4bf59792b6570e32e6d24635d4f5e5ac3
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829143"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4의 함수
====================
[Mike Wasson](https://github.com/MikeWasson)

> OData에서 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에는 Web API 2.2를 사용 하 여 OData v4 끝점 동작 및 함수를 추가 하는 방법을 보여 줍니다. 이 자습서를 기반으로 자습서 [OData v4 끝점 사용 하 여 ASP.NET Web API 2 만들기](create-an-odata-v4-endpoint.md)
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
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
> OData 버전 3을 참조 하세요 [ASP.NET Web API 2 OData 작업](../odata-v3/odata-actions.md)합니다.


차이점 *작업* 하 고 *함수* 작업 부작용이 있을 수 고 함수는 하지 않습니다. 동작과 함수 둘 다 데이터를 반환할 수 있습니다. 작업에 대 한 몇 가지 용도 다음과 같습니다.

- 복잡 한 트랜잭션입니다.
- 한 번에 여러 엔터티를 조작 합니다.
- 엔터티의 특정 속성에만 업데이트를 허용합니다.
- 엔터티가 아닌 데이터를 전송 합니다.

함수는 엔터티 또는 컬렉션에 직접 해당 하지 않는 정보를 반환 하는 데 유용 합니다.

작업 (또는 함수)는 단일 엔터티 또는 컬렉션을 지정할 수 있습니다. OData 용어에서이 합니다 *바인딩*합니다. 할 수도 있습니다 &quot;바인딩되지 않은&quot; 작업/함수를 서비스에 대 한 정적 작업으로 호출 됩니다.

## <a name="example-adding-an-action"></a>예: 작업 추가

제품을 평가 하는 작업을 정의 하겠습니다.

> [!NOTE]
> 이 자습서를 기반으로 한이 자습서 [OData v4 끝점 사용 하 여 ASP.NET Web API 2 만들기](create-an-odata-v4-endpoint.md)


첫째, 추가 `ProductRating` 등급을 나타내는 모델입니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

추가할 수도 **DbSet** 에 `ProductsContext` 클래스는 EF는 데이터베이스의 등급 테이블이 만들어집니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>EDM에 작업 추가

WebApiConfig.cs에서 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

합니다 **EntityTypeConfiguration.Action** 메서드는 EDM (엔터티 데이터 모델)에 작업을 추가 합니다. 합니다 **매개 변수** 메서드는 작업에 대 한 형식화 된 매개 변수를 지정 합니다.

또한이 코드는 EDM에 대 한 네임 스페이스를 설정합니다. 네임 스페이스 작업에 대 한 URI 작업 정규화 된 이름을 포함 하기 때문에 중요 합니다.

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 일반적인 IIS 구성에서이 URL에 있는 점을 404 오류를 반환 하는 IIS 발생 합니다. Web.Config 파일에 다음 섹션을 추가 하 여이 해결할 수 있습니다.

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>작업에 대 한 컨트롤러 메서드를 추가 합니다.

사용 하도록 설정 합니다 &quot;속도&quot; 작업을 다음 메서드를 추가 `ProductsController`:

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

메서드 이름이 작업 이름과 일치 하는지 확인 합니다. 합니다 **[HttpPost]** 특성이 지정 된 메서드는 HTTP POST 메서드입니다.

클라이언트는 작업을 호출 하려면 다음과 같이 HTTP POST 요청을 보냅니다.

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

합니다 &quot;속도&quot; 작업 제품 인스턴스에 바인딩되어 않기 때문에 작업에 대 한 URI는 정규화 된 작업 이름을 엔터티 URI에 추가 합니다. (EDM 네임 스페이스 설정 하 회수 &quot;ProductService&quot;이므로 작업 정규화 된 이름이 &quot;ProductService.Rate&quot;.)

요청 본문 JSON 페이로드로 작업 매개 변수를 포함합니다. 웹 API에 JSON 페이로드를 자동으로 변환 합니다는 **ODataActionParameters** 개체 매개 변수 값의 사전 뿐입니다. 컨트롤러 메서드에서 매개 변수에 액세스 하려면이 사전을 사용 합니다.

클라이언트에서 잘못 된 작업 매개 변수를 보내는 경우, 값의 형식을 **ModelState.IsValid** 은 false입니다. 컨트롤러 메서드에서이 플래그를 확인 하 고 오류가 반환 **IsValid** 은 false입니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>예: 함수를 추가합니다.

이제 가장 저렴 한 제품을 반환 하는 OData 함수를 추가 해 보겠습니다. 이전에 첫 번째 단계는 EDM에 함수를 추가 합니다. WebApiConfig.cs에서 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

이 경우 함수는 개별 제품 인스턴스가 아닌 제품 컬렉션에 바인딩됩니다. 클라이언트는 GET 요청을 전송 하 여 함수를 호출 합니다.

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

메서드 이름은 함수 이름과 일치 하는지 확인 합니다. 합니다 **[HttpGet]** HTTP GET 메서드는 특성을 지정 합니다.

HTTP 응답에는 다음과 같습니다.

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>예: 바인딩되지 않은 함수를 추가 하기

이전 예제에서 컬렉션에 바인딩된 함수. 다음 예제에서는 만듭니다는 *바인딩되지 않은* 함수입니다. 바인딩되지 않은 함수는 서비스에 대 한 정적 작업으로 호출 됩니다. 이 예제 함수는 지정 된 우편 번호에 대 한 판매 세금 반환 됩니다.

WebApiConfig 파일에서 EDM에 함수를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

호출 하는 것입니다 **함수** 에 직접 합니다 **된 ODataModelBuilder**, 엔터티 형식 또는 컬렉션을 대신 합니다. 이렇게 하면 함수는 바인딩된 모델 작성기입니다.

함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

이 메서드를 배치 하는 Web API 컨트롤러는 중요 하지 않습니다. 에 배치할 수 있습니다 `ProductsController`, 또는 별도 컨트롤러를 정의 합니다. 합니다 **[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.

클라이언트 요청 예제는 다음과 같습니다.

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 응답:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
