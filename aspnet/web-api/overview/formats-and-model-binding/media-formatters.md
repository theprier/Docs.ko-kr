---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2의에서 미디어 포맷터 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: 7b7ba2fb3f1bba0447e700c84a017266cba305e6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829070"
---
<a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2의에서 미디어 포맷터
====================
[Mike Wasson](https://github.com/MikeWasson)

이 자습서에는 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.

## <a name="internet-media-types"></a>인터넷 미디어 유형

데이터의 형식을 식별 하는 라고도 함은 MIME 형식이 미디어 유형입니다. HTTP, 미디어 유형 메시지 본문의 형식을 설명합니다. 미디어 유형을 두 문자열, 형식 및 하위 형식으로 구성 됩니다. 예를 들어:

- 텍스트/html
- 이미지/png
- application/json

HTTP 메시지에 엔터티 본문이 포함 된 경우 콘텐츠 형식 헤더를 메시지 본문의 형식을 지정 합니다. 이렇게 하면 수신자가 메시지 본문의 내용을 구문 분석 하는 방법.

예를 들어, PNG 이미지를 포함 하는 HTTP 응답을 하는 경우 응답 머리글이 해야 할 수 있습니다.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

클라이언트 요청 메시지를 보내면 Accept 헤더를 포함할 수 있습니다. Accept 헤더는 미디어 유형의 클라이언트 server가 서버에서 알려 줍니다. 예를 들어:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

이 헤더 클라이언트가 HTML, XHTML 또는 XML는 서버를 알려 줍니다.

미디어 유형에 Web API serialize 하 고 HTTP 메시지 본문을 deserialize 하는 방법을 결정 합니다. 웹 API는 XML, JSON, BSON을 및 양식 urlencoded 데이터에 대 한 기본 제공 및 작성 하 여 추가 미디어 형식을 지원할 수 있습니다는 *미디어 포맷터*합니다.

미디어 포맷터를 만들려면 이러한 클래스 중 하나에서 파생 됩니다.

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx). 이 클래스는 비동기 읽기 및 쓰기 메서드.
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx). 이 클래스에서 파생 됩니다 **MediaTypeFormatter** sychronous 읽기/쓰기 메서드를 사용 합니다.

파생 **BufferedMediaTypeFormatter** 비동기 코드가 없는 것 이지만 I/O 하는 동안 호출 스레드가 차단할 수 있으므로 더 간단 합니다.

## <a name="example-creating-a-csv-media-formatter"></a>예: 만들기, CSV 미디어 포맷터

다음 예제에서는 쉼표로 구분 된 값 (CSV) 형식으로 제품 개체를 serialize 할 수 있는 미디어 유형 포맷터를 보여 줍니다. 이 예제에서는 자습서에 정의 된 제품 유형이 [Web API에서는 CRUD 작업을 만드는](../older-versions/creating-a-web-api-that-supports-crud-operations.md)합니다. Product 개체의 정의 다음과 같습니다.

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

CSV 포맷터를 구현 하려면에서 파생 된 클래스를 정의 **BufferedMediaTypeFormater**:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

생성자에서 포맷터가 지 원하는 미디어 유형에 추가 합니다. 이 예제에서는 포맷터는 단일 미디어 형식이 지 원하는 &quot;텍스트/c s v&quot;:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

재정의 된 **CanWriteType** 포맷터는 형식을 나타내는 방법 serialize 할 수 있습니다.

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

이 예제에서는 포맷터를 serialize 할 수 단일 `Product` 개체의 컬렉션 뿐만 아니라 `Product` 개체입니다.

마찬가지로, 재정의 **CanReadType** 포맷터는 형식을 나타내기 위해 메서드를 deserialize 할 수 있습니다. 이 예제에서는 포맷터를 지원 하지 않으므로 deserialization 메서드는 단순히 반환 **false**합니다.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

마지막으로 재정의 된 **WriteToStream** 메서드. 이 메서드는 스트림에 작성 하 여 형식을 serialize 합니다. 포맷터가 deserialization을 지 원하는 경우 재정의할 수도 합니다 **ReadFromStream** 메서드.

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>미디어 포맷터를 Web API 파이프라인에 추가

미디어 유형 포맷터를 Web API 파이프라인을 추가 하려면 사용 합니다 **포맷터** 속성에는 **HttpConfiguration** 개체.

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>문자 인코딩

필요에 따라 미디어 포맷터를 u t F-8에서 ISO 8859-1 등 여러 문자 인코딩을 지원할 수 있습니다.

생성자에서 하나 이상의 추가 [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) 형식에 **SupportedEncodings** 컬렉션입니다. 첫 번째 인코딩 기본값을 배치 합니다.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

에 **WriteToStream** 하 고 **ReadFromStream** 메서드를 호출 [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) 기본 문자 인코딩을 선택 합니다. 이 메서드는 지원 되는 인코딩 목록에 대 한 요청 헤더와 일치합니다. 사용 하 여 반환 된 **Encoding** 읽거나 스트림에서 쓰기:

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
