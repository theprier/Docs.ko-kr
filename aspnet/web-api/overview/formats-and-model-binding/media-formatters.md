---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: "ASP.NET Web API 2의에서 미디어 포맷터 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: 7d85b995cd577d0ff90fe96bce508c7fbdc6ebbb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2의에서 미디어 포맷터
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 자습서에서는 ASP.NET Web API에서 추가 미디어 형식을 방법을 지원합니다.

## <a name="internet-media-types"></a>인터넷 미디어 유형

데이터의 형식을 식별 하는 MIME 형식이 라고도 하는 미디어 유형입니다. HTTP, 미디어 유형에 대해 메시지 본문의 형식은 설명합니다. 미디어 유형은 두 문자열, 형식 및 하위 구성 됩니다. 예:

- html 텍스트 /
- 이미지/png
- application/json

HTTP 메시지에 엔터티 본문이 포함 되어 있으면, 콘텐츠 형식 헤더는 메시지 본문의 형식을 지정 합니다. 이렇게 하면 수신자는 메시지 본문의 내용을 구문 분석 하는 방법입니다.

예를 들어 PNG 이미지를 포함 하는 HTTP 응답을 응답에 다음 헤더 할 수 있습니다.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

클라이언트 요청 메시지를 보내면 Accept 헤더를 포함할 수 있습니다. Accept 헤더는 미디어 유형의 클라이언트 서버는 서버에서 원하는 지시 합니다. 예:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

이 헤더 클라이언트가 HTML, XHTML 또는 XML을 서버에 알려 줍니다.

미디어 유형 웹 API를 직렬화 및 역직렬화 HTTP 메시지 본문 방법을 결정 합니다. Web API에서 기본적으로 XML, JSON, BSON, 및 양식 인코딩된 데이터를 지원 하 고 작성 하 여 추가 미디어 유형을 지원할 수 있습니다는 *미디어 포맷터*합니다.

미디어 포맷터를 만들려면 이러한 클래스 중 하나에서 파생 됩니다.

- [MediaTypeFormatter](https://msdn.microsoft.com/en-us/library/system.net.http.formatting.mediatypeformatter.aspx)합니다. 이 클래스는 비동기 읽기 및 쓰기 메서드.
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/en-us/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)합니다. 이 클래스에서 파생 **MediaTypeFormatter** 하지만 sychronous 읽기/쓰기 메서드를 사용 합니다.

파생 된 **BufferedMediaTypeFormatter** 은 코드가 없는 비동기 I/O 중 호출 스레드를 차단할 수 의미 하기 때문에 더 간단 합니다.

## <a name="example-creating-a-csv-media-formatter"></a>예: CSV 미디어 포맷터 생성

다음 예제를 쉼표로 구분 된 값 (CSV) 형식에서 제품 개체를 serialize 할 수 있는 미디어 유형 포맷터를 보여줍니다. 이 예제에서는 자습서에 정의 된 제품 유형을 사용 하 여 [CRUD 작업을 지원 합니다. 해당 웹 API를 만드는](../older-versions/creating-a-web-api-that-supports-crud-operations.md)합니다. 제품 개체의 정의 다음과 같습니다.

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

파생 되는 클래스 정의 CSV 포맷터를 구현 하려면 **BufferedMediaTypeFormater**:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

생성자에 포맷터가 지 원하는 미디어 유형에 추가 합니다. 포맷터가 단일 미디어 형식을 지 원하는이 예제에서는 &quot;텍스트/csv&quot;:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

재정의 **CanWriteType** 포맷터 유형을 나타내도록 메서드를 serialize 할 수 있습니다.

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

이 예제에서는 포맷터를 serialize 할 수 단일 `Product` 개체의 컬렉션 뿐만 아니라 `Product` 개체입니다.

마찬가지로, 재정의 **CanReadType** 포맷터 유형을 나타내도록 메서드를 역직렬화 할 수 있습니다. 이 예제에서는 포맷터 지원 하지 않습니다 deserialization 메서드는 단순히 반환 하므로 **false**합니다.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

마지막으로, 재정의 **WriteToStream** 메서드. 이 메서드는 스트림에 작성 하 여 형식을 serialize 합니다. 포맷터가 deserialization을 지 원하는 경우 재정의 **ReadFromStream** 메서드.

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>Web API 파이프라인에 미디어 포맷터를 추가합니다.

미디어 유형 포맷터를 Web API 파이프라인을 추가 하려면 사용 된 **포맷터** 속성에는 **HttpConfiguration** 개체입니다.

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>문자 인코딩

필요에 따라 미디어 포맷터는 ISO 8859-1 또는 u t F-8와 같은 여러 문자 인코딩을 지원할 수 있습니다.

생성자를 하나 이상 추가 [System.Text.Encoding](https://msdn.microsoft.com/en-us/library/system.text.encoding.aspx) 형식을 **SupportedEncodings** 컬렉션입니다. 기본을 인코딩 첫 번째 넣습니다.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

에 **WriteToStream** 및 **ReadFromStream** 메서드를 호출 [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/en-us/library/hh969054.aspx) 기본 문자 인코딩을 선택할 수 있습니다. 이 메서드는 지원 되는 인코딩 목록에 대해 요청 헤더와 일치합니다. 사용 하 여 반환 된 **인코딩** 읽거나 쓸 스트림의:

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
