---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API의에서 협상 내용 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API HTTP 콘텐츠 협상을 구현 하는 방법에 대해 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/20/2012
ms.topic: article
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: ca373af6754e82889dc100b63f73b76aaa4e4f27
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26507022"
---
<a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API의에서 콘텐츠 협상
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API에서 콘텐츠 협상을 구현 하는 방법을 설명 합니다.

"여러 표현이 있는 경우 지정 된 응답에 대 한 가장 잘 표시를 선택 하는 프로세스입니다."와 콘텐츠 협상을 정의 하는 HTTP 사양 (RFC 2616) Http에서 콘텐츠 협상에는 기본 메커니즘은 이러한 요청 헤더

- **수락:** 미디어 유형을 "application/json이"와 같은 응답에 대 한 허용 되는 "application/xml," 또는와 같은 사용자 지정 미디어 유형을 &quot;application/vnd.example+xml&quot;
- **Accept-charset:** 는 문자 집합은 같은 utf-8 또는 ISO 8859-1입니다.
- **허용 인코딩:** 콘텐츠 인코딩을 gzip과 같은 허용 됩니다.
- **수락 언어:** 기본 자연어와 같은 "en-us"입니다.

서버는 HTTP 요청의 다른 부분 살펴볼 수도 있습니다. 예를 들어 X-요청한-와 헤더를 포함 하는 요청을 하는 경우 AJAX 요청을 나타내는 서버 기본적으로 JSON Accept 헤더가 없습니다.

이 문서에서는 웹 API 적용 및 Accept-charset 헤더를 사용 하는 방법을 살펴보겠습니다. (지금은 있습니다 Accept-encoding 또는 Accept-language에 대 한 기본 제공 지원이.)

## <a name="serialization"></a>Serialization

CLR 형식으로 리소스를 반환 하는 Web API 컨트롤러, 파이프라인 반환 값 또는 그 반대로 serialize 하 고 HTTP 응답 본문에 씁니다.

예를 들어 컨트롤러 동작:

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

클라이언트가이 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

에 대 한 응답 서버 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

이 예제에서는 클라이언트 요청 JSON, Javascript, 또는 "항목" (\*/\*). 응답의 JSON 표현으로 받은 서버는 `Product` 개체입니다. 응답에서 Content-type 헤더가로 설정 되는 &quot;응용 프로그램/json&quot;합니다.

컨트롤러를 반환할 수도 있습니다는 **HttpResponseMessage** 개체입니다. 응답 본문에 대 한 CLR 개체를 지정 하려면 호출는 **CreateResponse** 확장 메서드:

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

이 옵션에는 응답의 세부 사항에 대해 더 많은 제어할 수 있습니다. 상태 코드를 설정 하 고을 HTTP 헤더를 추가 하 고, 등 수 있습니다.

리소스를 직렬화 하는 개체 라고는 *미디어 포맷터*합니다. 미디어 포맷터가 파생 되는 **MediaTypeFormatter** 클래스입니다. Web API 미디어 포맷터 XML 및 JSON을 하며 다른 미디어 형식을 지원 하기 위해 사용자 지정 포맷터를 만들 수 있습니다. 사용자 지정 포맷터를 작성 하는 방법에 대 한 정보를 참조 하십시오. [미디어 포맷터](media-formatters.md)합니다.

## <a name="how-content-negotiation-works"></a>콘텐츠 협상 작동

첫째, 파이프라인 가져옵니다는 **IContentNegotiator** 서비스는 **HttpConfiguration** 개체입니다. 또한 미디어 포맷터에서의 목록을 가져옵니다는 **HttpConfiguration.Formatters** 컬렉션입니다.

그런 다음 파이프라인 호출 **IContentNegotiatior.Negotiate**을 전달 합니다.

- 직렬화 할 개체의 유형
- 미디어 포맷터의 컬렉션
- HTTP 요청

**Negotiate** 메서드는 두 가지 정보를 반환 합니다.

- 사용 하는 포맷터
- 응답에 대 한 미디어 유형

포맷터가 있으면는 **Negotiate** 메서드 반환 **null**, 클라이언트 받는 HTTP 오류 406 (승인 금지).

다음 코드는 컨트롤러 콘텐츠 협상 수 직접 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

이 코드는 해당 하는 파이프라인에서 자동으로 수행 합니다.

## <a name="default-content-negotiator"></a>기본 콘텐츠 협상 자입니다.

**DefaultContentNegotiator** 클래스의 기본 구현을 제공 **IContentNegotiator**합니다. 다양 한 조건을 사용 하 여 포맷터를 선택 합니다.

첫째, 포맷터 형식을 직렬화 할 수 있어야 합니다. 이 호출 하 여 확인 됩니다 **MediaTypeFormatter.CanWriteType**합니다.

다음으로 콘텐츠 협상 자 각 포맷터에 얼마나 잘 HTTP 요청을 일치를 평가 합니다. 일치 하는 평가 하 고, 콘텐츠 협상 자 기능에서는 다음 두 가지 포맷터에:

- **SupportedMediaTypes** 지원 되는 미디어 형식 목록이 포함 된 컬렉션입니다. 콘텐츠 협상 자 요청 Accept 헤더에 대해이 목록에 일치 시 키 려 합니다. 참고 Accept 헤더가 범위를 포함할 수 있습니다. 예를 들어 "텍스트/plain"은 텍스트와 일치 하는 /\* 또는 \* / \*합니다.
- **MediaTypeMappings** 목록을 포함 하는 컬렉션 **MediaTypeMapping** 개체입니다. **MediaTypeMapping** 클래스는 HTTP 요청을 미디어 형식과 일치 하는 일반적인 방법을 제공 합니다. 예를 들어 특정 미디어 유형에 사용자 지정 HTTP 헤더를 매핑할 수 것입니다.

여러 개의 일치, 최고 품질 비율 wins와 일치 합니다. 예를 들어:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

이 예제에서는 응용 프로그램/json에 응용 프로그램/xml을 통해 기본 있으므로 1.0은 암시적된 품질 요소입니다.

일치 하는 경우 콘텐츠 협상 자 다시 일치 하는 요청 본문의 미디어 형식에 있는 경우. 예를 들어, JSON 데이터를 포함 하는 요청을 콘텐츠 협상 자 JSON 포맷터를 찾습니다.

남아 있는 경우 일치 하는 항목, 콘텐츠 협상 자는 단순히 형식을 serialize 할 수 있는 첫 번째 포맷터를 선택 합니다.

## <a name="selecting-a-character-encoding"></a>문자 인코딩을 선택

콘텐츠 협상 자 최상의 문자 인코딩을 확인 하 여 선택 하는 포맷터를 선택한 후는 **SupportedEncodings** 포맷터 및 (있는 경우) 요청에 Accept-charset 헤더에 대해 검색 속성입니다.
