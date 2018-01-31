---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: "ASP.NET Web API 2.1의에서 BSON 지원 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 53ad705fad6d2225cecca4d73355bd6ebfcf56d5
ms.sourcegitcommit: 459cb3289741a3f46325e605a617dc926ee0563d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
<a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1의에서 BSON 지원
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

Web API 2.1에서는 BSON 지원 합니다. 이 항목에서는 Web API 컨트롤러 (서버 쪽) 및.NET 클라이언트 앱 BSON을 사용 하는 방법을 보여 줍니다.

## <a name="what-is-bson"></a>BSON 란?

[BSON](http://bsonspec.org/) 은 이진 serialization 형식입니다. "BSON"은 "Binary JSON" 있지만 BSON 및 JSON 매우 다르게 serialize 됩니다. BSON은 "JSON 유사한" 이므로 개체를 JSON 비슷한 이름-값 쌍으로 표현 됩니다. JSON, 달리 숫자 데이터 형식이 문자열이 아니라를 바이트로 저장

BSON 가볍고, 스캔 하기 쉬운 인코딩/디코딩에 빠른 되도록 설계 되었습니다.

- BSON는 JSON 크기가 유사 합니다. 데이터에 따라 BSON 페이로드 JSON 페이로드 보다 크거나 작을 수 있습니다. 이미지 파일과 같은 이진 데이터를 직렬화 하는 작업에 대 한 없기 때문에 이진 데이터가 base64 인코딩 BSON는 JSON, 보다 작습니다.
- BSON 문서는 쉽게 요소 라는 접두사가 길이 필드 이므로 파서에서 디코딩하지 않고도 요소를 건너뛸 수 때문에 검색할 수 있습니다.
- 인코딩 및 디코딩하는 숫자 데이터 형식이 문자열이 아니라 숫자로 저장 되기 때문에, 효율적입니다.

.NET 클라이언트 앱 등의 네이티브 클라이언트 BSON JSON 또는 XML과 같은 텍스트 기반 형식 대신 사용 하 여 이점을 얻을 수 있습니다. 브라우저 클라이언트에 대 한 싶을 것 환경에 JSON, JavaScript JSON 페이로드를 직접 변환할 수 있습니다.

웹 API에 사용 다행히 [콘텐츠 협상](content-negotiation.md)하므로 API에서 두 가지 형식 모두를 지원 하 고 선택 하면 클라이언트 수, 합니다.

## <a name="enabling-bson-on-the-server"></a>BSON 서버에서 사용 하도록 설정

Web API 구성에 추가 **BsonMediaTypeFormatter** 포맷터 컬렉션에 있습니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

이제는 클라이언트가 "응용 프로그램/bson"를 요청 하는 경우 웹 API BSON 포맷터를 사용 합니다.

BSON 다른 미디어 유형에 연결할 SupportedMediaTypes 컬렉션에 추가 합니다. 다음 코드는 지원 되는 미디어 형식에 "application/vnd.contoso"를 추가 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>HTTP 세션 예제

이 예에서는 간단한 Web API 컨트롤러 및 다음과 같은 모델 클래스를 사용 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

클라이언트는 다음 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

다음은 응답이입니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

여기에서 이진 데이터를 바꾸어도 &quot;.&quot; 문자입니다. 다음 스크린 샷에서 원시 16 진수 값에서 Fiddler 보여 줍니다.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>BSON HttpClient 사용

.NET 클라이언트 앱 BSON 포맷터를 사용할 수 있습니다 **HttpClient**합니다. 에 대 한 자세한 내용은 **HttpClient**, 참조 [웹 API에서 정도.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.

다음 코드는 BSON을 받아들이고 다음 응답에 BSON 페이로드를 역직렬화 하는 GET 요청을 보냅니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

BSON을 서버에서 요청 하려면 Accept 헤더 "응용 프로그램/bson"를 설정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

응답 본문을 deserialize 하는 데 사용 된 **BsonMediaTypeFormatter**합니다. 이 포맷터 하지 않으므로 기본 포맷터 컬렉션에서 응답 본문을 읽을 때 지정 해야 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

다음 예제에서는 BSON 포함 된 POST 요청을 전송 하는 방법을 보여 줍니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

이 코드의 대부분은 앞의 예제와 같습니다. 하지만 **PostAsync** 메서드를 지정 **BsonMediaTypeFormatter** 포맷터로:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>최상위 기본 형식 직렬화

모든 BSON 문서는 키/값 쌍의 목록입니다. BSON 사양에는 정수 또는 문자열과 같은 단일 원시 값을 직렬화 하는 작업에 대 한 구문을 정의 하지 않습니다.

이 제한을 해결 하는 **BsonMediaTypeFormatter** 특별 한 경우 기본 형식 취급 합니다. 직렬화 하는 작업을 하기 전에 변환 값 키/값 쌍으로 "Value" 키를 가진 합니다. 예를 들어 정수를 반환 하는 API 컨트롤러 있다고 가정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

직렬화 하는 작업을 하기 전에 BSON 포맷터 키/값 쌍에 변환 합니다.

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Deserialize 하면 포맷터 원래 값으로 다시 데이터를 변환 합니다. 그러나 다른 BSON 파서를 사용 하 여 클라이언트는 web API 원시 값을 반환 하는 경우이 경우를 처리 하 있어야 합니다. 일반적으로 원시 값 보다는 구조화 된 데이터를 반환 하는 것이 좋습니다.

## <a name="additional-resources"></a>추가 리소스

[웹 API BSON 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[미디어 포맷터](media-formatters.md)
