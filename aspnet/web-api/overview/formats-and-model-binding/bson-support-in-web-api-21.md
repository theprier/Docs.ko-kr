---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1에서에서 BSON 지원 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 7c5e763d92295a83b3431e9ec6e305b07f8a64d2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370496"
---
<a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1에서에서 BSON 지원
====================
[Mike Wasson](https://github.com/MikeWasson)

Web API 2.1에서는 BSON 지원 합니다. 이 항목에서는 Web API 컨트롤러 (서버 쪽) 및.NET 클라이언트 앱에서 BSON을 사용 하는 방법을 보여 줍니다.

## <a name="what-is-bson"></a>BSON 란?

[BSON](http://bsonspec.org/) 은 이진 serialization 형식입니다. "BSON"는 "이진 JSON"를 의미 하지만 BSON 및 JSON 매우 다른 방식으로 serialize 됩니다. BSON은 "JSON 유사한" 하므로 개체는 JSON과 유사한 이름-값 쌍으로 표시 됩니다. JSON에서와 달리 숫자 데이터 형식 문자열이 아니라 바이트로 저장 됩니다.

BSON 가볍고, 검색이 용이 인코딩/디코딩 속도가 되도록 설계 되었습니다.

- BSON은 JSON에 크기와 비슷합니다. 데이터에 따라 BSON 페이로드는 JSON 페이로드 보다 작거나 클 수 있습니다. 이미지 파일과 같은 이진 데이터를 직렬화 하는 작업에 대 한 없기 때문에 이진 데이터가 base64로 인코딩된 BSON은 JSON 보다 작습니다.
- BSON 문서는 요소 길이 필드를 사용 하 여 접두사가 파서를 고를 디코딩하지 않고도 요소를 건너뛸 수 있도록 하기 때문에 스캔 쉽습니다.
- 인코딩 및 디코딩 되므로 효율적인 숫자 문자열이 아니라 숫자 데이터 형식이 저장 됩니다.

.NET 클라이언트 앱과 같은 네이티브 클라이언트에서 BSON을 사용 하 여 JSON 또는 XML과 같은 텍스트 기반 형식 대신 이용할 수 있습니다. 브라우저 클라이언트에는 아마도 JSON을 사용 하 있으므로 원하는 JavaScript JSON 페이로드에 직접 변환할 수 있습니다.

다행 스럽게도 Web API 사용 [콘텐츠 협상](content-negotiation.md)API 두 형식을 모두 지원 하 고 선택할 클라이언트 수 있도록 합니다.

## <a name="enabling-bson-on-the-server"></a>서버에서 BSON을 사용 하도록 설정

Web API 구성에 추가 합니다 **BsonMediaTypeFormatter** 포맷터 컬렉션에 있습니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

이제 클라이언트는 "application/bson"을 요청 하는 경우 웹 API는 BSON 포맷터를 사용 합니다.

BSON 다른 미디어 유형을 연결할 SupportedMediaTypes 컬렉션에 추가 합니다. 다음 코드는 지원 되는 미디어 유형으로 "application/vnd.contoso"를 추가합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>예제에서는 HTTP 세션

이 예에서는 간단한 Web API 컨트롤러 및 다음 모델 클래스:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

클라이언트는 다음 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

응답은 다음과 같습니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

여기서 사용 하 여 이진 데이터를 바꿨습니다 &quot;.&quot; 문자입니다. 다음 스크린 샷에서 원시 16 진수 값에서 Fiddler 보여 줍니다.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>HttpClient를 사용 하 여 BSON을 사용 하 여

.NET 클라이언트 앱에는 BSON 포맷터를 사용할 수 있습니다 **HttpClient**합니다. 에 대 한 자세한 내용은 **HttpClient**를 참조 하세요 [웹 API에서는.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.

다음 코드는 BSON을 받고 응답에서 BSON 페이로드 개체를 deserialize 하는 GET 요청을 보냅니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

서버에서 BSON을 요청 하려면 "application/bson" Accept 헤더를 설정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

응답 본문을 deserialize 하는 데 사용 합니다 **BsonMediaTypeFormatter**합니다. 이 포맷터 아니므로 기본 포맷터 컬렉션에서 응답 본문을 읽을 때 지정 해야 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

다음 예제에서는 BSON을 포함 하는 POST 요청을 전송 하는 방법을 보여 줍니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

이 코드의 대부분 이전 예제와 동일합니다. 하지만 합니다 **PostAsync** 메서드를 지정 **BsonMediaTypeFormatter** 포맷터로:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>최상위 기본 형식 직렬화

모든 BSON 문서에는 키/값 쌍의 목록입니다. BSON 사양에는 정수나 문자열 같은 단일 원시 값을 직렬화 하는 작업에 대 한 구문을 정의 하지 않습니다.

이 제한을 해결 하는 **BsonMediaTypeFormatter** 특별 한 경우 기본 형식 취급 합니다. 직렬화 하는 작업을 하기 전에 값을 변환 키/값 쌍을 키 "값"를 사용 하 여 합니다. 예를 들어, API 컨트롤러는 정수를 반환 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

직렬화 하는 작업을 하기 전에 BSON 포맷터 다음 키/값 쌍으로 변환:

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Deserialize 할 때는 포맷터 원래 값으로 다시 데이터를 변환 합니다. 그러나 다른 BSON 파서를 사용 하 여 클라이언트에 web API는 원시 값을 반환 하는 경우이 경우를 처리 하도록 해야 합니다. 일반적으로 원시 값이 아니라 구조화 된 데이터를 반환 하는 것이 좋습니다.

## <a name="additional-resources"></a>추가 리소스

[웹 API BSON 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[미디어 포맷터](media-formatters.md)
