---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: 콘텐츠 협상 ASP.NET Web API에서에서 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API HTTP 콘텐츠 협상을 구현 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/20/2012
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: e936bdfa52f786ec86d3e84eac3cd644225b6f92
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835183"
---
<a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API에서에서 콘텐츠 협상
====================
[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API에서 콘텐츠 협상을 구현 하는 방법을 설명 합니다.

"여러 표현이 있는 경우 지정된 된 응답에 대 한 최상의 표현을 선택 하는 프로세스입니다."와 콘텐츠 협상을 정의 하는 HTTP 사양 (RFC 2616) Http에서 콘텐츠 협상을 위한 기본 메커니즘은 이러한 요청 헤더:

- **수락:** 미디어 유형을 "application/json이"와 같은 응답에 허용 되는 "application/xml" 또는 같은 사용자 지정 미디어 형식이 &quot;application/vnd.example+xml&quot;
- **Accept-charset:** 문자 집합을 u t F-8에서 ISO 8859-1 등 허용 됩니다.
- **허용 인코딩:** 콘텐츠 인코딩을 gzip과 같은 허용 됩니다.
- **수용-언어:** 기본 자연 언어를 같은 "en-우리"입니다.

HTTP 요청의 다른 부분에서 서버를 찾아볼 수도 있습니다. 예를 들어 X-요청-사용 하 여 헤더를 포함 하는 요청을 하는 경우 AJAX 요청을 나타내는 서버 기본적으로 JSON Accept 헤더가 없는 경우.

이 문서에서는 웹 API의 수락 및 Accept-charset 헤더를 사용 하는 방법을 살펴보겠습니다. (지금은 경우 Accept-encoding 또는 수용-언어에 대 한 기본 제공 지원 없음)

## <a name="serialization"></a>Serialization

CLR 형식으로 리소스를 반환 하는 Web API 컨트롤러, 파이프라인 반환 값을 serialize 하 고 HTTP 응답 본문에 씁니다.

예를 들어 다음 컨트롤러 작업을 고려 합니다.

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

클라이언트는이 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

서버를 응답으로 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

이 예제에서는 클라이언트 요청 JSON, Javascript 또는 "anything" (\*/\*). 응답의 JSON 표현으로 받은 서버는 `Product` 개체입니다. 응답의 Content-type 헤더에 설정 됩니다 &quot;application/json&quot;합니다.

컨트롤러를 반환할 수도 있습니다는 **HttpResponseMessage** 개체입니다. 응답 본문에 대 한 CLR 개체를 지정 하려면 호출을 **CreateResponse** 확장 메서드:

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

이 옵션은 응답의 세부 정보를 보다 자세히 제어를 제공 합니다. 상태 코드를 설정 하 고, HTTP 헤더를 추가 하 고, 등 수 있습니다.

리소스를 serialize 하는 개체를 *미디어 포맷터*합니다. 미디어 포맷터에서 파생 된 **MediaTypeFormatter** 클래스입니다. Web API는 XML 및 JSON에 대 한 미디어 포맷터를 제공 하 고 다른 미디어 형식을 지원 하기 위해 사용자 지정 포맷터를 만들 수 있습니다. 사용자 지정 포맷터를 작성 하는 방법에 대 한 내용은 [미디어 포맷터](media-formatters.md)합니다.

## <a name="how-content-negotiation-works"></a>콘텐츠 협상 작동

먼저, 파이프라인을 가져옵니다 합니다 **IContentNegotiator** 서비스를 **HttpConfiguration** 개체입니다. 미디어 포맷터 목록을 가져옵니다 합니다 **HttpConfiguration.Formatters** 컬렉션입니다.

다음으로 파이프라인을 호출 **IContentNegotiatior.Negotiate**를 전달 합니다.

- Serialize 할 개체의 형식
- 미디어 포맷터의 컬렉션
- HTTP 요청

합니다 **Negotiate** 메서드는 두 가지 정보를 반환 합니다.

- 사용 하는 포맷터
- 응답에 대 한 미디어 유형

포맷터가 있으면 합니다 **Negotiate** 메서드가 반환 **null**, 클라이언트 받는 HTTP 오류 406 (허용 되지 않음).

다음 코드는 컨트롤러 콘텐츠 협상 수 직접 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

이 코드는 해당 하는 파이프라인에서 자동으로 수행 합니다.

## <a name="default-content-negotiator"></a>기본 콘텐츠 협상 자입니다.

합니다 **DefaultContentNegotiator** 클래스의 기본 구현을 제공 **IContentNegotiator**합니다. 여러 조건을 사용 하 여 포맷터 선택.

먼저 포맷터는 형식을 serialize 할 수 있어야 합니다. 호출 하 여 확인 되 **MediaTypeFormatter.CanWriteType**합니다.

다음으로 콘텐츠 협상 자를 각 포맷터 살펴봅니다 얼마나 잘 HTTP 요청을 일치 하는지를 평가 합니다. 일치 항목을 평가 하려면 콘텐츠 협상 자는 두 가지 포맷터의에 살펴봅니다.

- 합니다 **SupportedMediaTypes** 지원 되는 미디어 유형 목록을 포함 하는 컬렉션입니다. 콘텐츠 협상 자 요청 Accept 헤더에 대해이 목록과 일치 하도록 시도 합니다. 참고 Accept 헤더가 범위를 포함할 수 있습니다. 예를 들어, "텍스트/plain"은 텍스트와 일치 하는 /\* 나 \* / \*합니다.
- 합니다 **MediaTypeMappings** 의 목록을 포함 하는 컬렉션 **MediaTypeMapping** 개체입니다. 합니다 **MediaTypeMapping** 클래스는 HTTP 요청을 미디어 유형과 일치 하는 일반적인 방법을 제공 합니다. 예를 들어, 사용자 지정 HTTP 헤더를 특정 미디어 형식에 매핑할 수 있습니다.

여러 개 있을 경우 일치, 최고 품질 비율 wins 사용 하 여 일치 합니다. 예를 들어:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

이 예제에서는 application/json 있으므로 1.0 묵시적된 품질 요소를이 application/xml 보다 선호 됩니다.

일치 하는 경우 콘텐츠 협상 자 있는 경우 요청 본문의 미디어 유형에 일치 하도록 시도 합니다. 예를 들어 요청 JSON 데이터가 포함 된 경우 콘텐츠 협상 자 JSON 포맷터를 찾습니다.

남아 있는 경우 일치 하는 항목을 콘텐츠 협상 자는 단순히 형식을 serialize 할 수 있는 첫 번째 포맷터를 선택 합니다.

## <a name="selecting-a-character-encoding"></a>문자 인코딩을 선택합니다.

콘텐츠 협상 자를 확인 하 여 최적의 문자 인코딩을 선택 포맷터를 선택한 후는 **SupportedEncodings** 포맷터 및 (있는 경우) 요청에 Accept-charset 헤더에 대 한 검색 속성입니다.
