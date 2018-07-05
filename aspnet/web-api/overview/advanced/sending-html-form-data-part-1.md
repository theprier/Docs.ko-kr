---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 양식 urlencoded 데이터 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/15/2012
ms.topic: article
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 24410c92df828d4aaaa3b91dd3e9fa14575fd300
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399872"
---
<a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 양식 urlencoded 데이터
====================
[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>1 부: 양식 urlencoded 데이터

이 문서에서는 Web API 컨트롤러에 양식 urlencoded 데이터를 게시 하는 방법을 보여 줍니다.

- [HTML 폼의 개요](#overview_of_html_forms)
- [보내는 복합 형식](#sending_complex_types)
- [AJAX 통해 양식 데이터 보내기](#sending_form_data_via_ajax)
- [보내는 단순 형식](#sending_simple_types)

> [!NOTE]
> [완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)합니다.


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML 폼의 개요

HTML 양식 사용 하 여 GET 또는 게시 서버로 데이터를 보내도록 합니다. **메서드** 특성을 **폼** HTTP 메서드를 제공 하는 요소:

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

기본 메서드는 GET입니다. 양식을 사용 하는 경우를 가져오려면 데이터를 URI 쿼리 문자열로 인코딩된 형식입니다. 폼 POST를 사용 하는 경우 양식 데이터가 요청 본문에 배치 됩니다. 게시 된 데이터에 대 한 합니다 **enctype** 특성 요청 본문의 형식을 지정 합니다.

| enctype | 설명 |
| --- | --- |
| application/x-www-form-urlencoded | 양식 데이터는 URI 쿼리 문자열로 비슷합니다 이름/값 쌍으로 인코딩됩니다. 게시물에 대 한 기본 형식입니다. |
| 다중 파트/폼 데이터 | 양식 데이터는 다중 파트 MIME 메시지를로 인코딩됩니다. 서버에 파일을 업로드 하는 경우이 형식을 사용 합니다. |

이 기사의 1 부 x-www-형식-urlencoded 형식에 살펴봅니다. [2 부](sending-html-form-data-part-2.md) 다중 파트 MIME에 설명 합니다.

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>보내는 복합 형식

일반적으로 여러 폼 컨트롤에서 가져온 값으로 구성 된 복합 형식에 보내집니다. 상태 업데이트를 나타내는 다음 모델을 고려 합니다.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

다음은 허용 하는 Web API 컨트롤러는 `Update` POST 통해 개체입니다.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> 이 컨트롤러를 사용 하 여 [동작 기반 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)이므로 경로 템플릿은 &quot;api / {컨트롤러} / {action} / {id}&quot;합니다. 클라이언트 데이터를 게시할 예정 &quot;/api/updates/complex&quot;합니다.


이제 상태 업데이트를 제출 하는 사용자에 대 한 HTML 폼을 작성해 보겠습니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

에 **작업** 양식의 특성이 컨트롤러 작업의 URI입니다. 폼에 입력 한 일부 값으로는 다음과 같습니다.

![](sending-html-form-data-part-1/_static/image1.png)

사용자가 제출 하는 경우 브라우저는 HTTP 요청을 유사한 다음 합니다.

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

요청 본문은 이름/값 쌍 형식으로 폼 데이터를 포함 하는 알 수 있습니다. 웹 API는 자동으로 이름/값 쌍의 인스턴스로 변환 합니다 `Update` 클래스입니다.

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>AJAX 통해 양식 데이터 보내기

사용자가 폼을 제출 하면 브라우저는 현재 페이지 밖으로 이동 하 고 응답 메시지의 본문을 렌더링 합니다. 이런 경우 확인 응답은 HTML 페이지입니다. 하지만 Web API 사용 응답 본문은 일반적으로 비어 있거나 JSON과 같은 구조화 된 데이터를 포함 합니다. 이 경우 편이 보낼 AJAX를 사용 하 여 폼 데이터 요청, 페이지 응답을 처리할 수 있도록 합니다.

다음 코드에는 jQuery를 사용 하 여 폼 데이터를 게시 하는 방법을 보여 줍니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **제출** 함수는 새 함수를 사용 하 여 form action을 대체 합니다. 이 제출 단추의 기본 동작을 재정의 합니다. 합니다 **serialize** 함수 이름/값 쌍에 양식 데이터를 serialize 합니다. 서버에 폼 데이터를 보내도록 호출 `$.post()`합니다.

요청이 완료 되 면 합니다 `.success()` 또는 `.error()` 처리기는 사용자에 게 적절 한 메시지를 표시 합니다.

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>보내는 단순 형식

이전 섹션에서는 Web API 모델 클래스의 인스턴스로 deserialize 하는 복합 형식을 보냈습니다. 또한 문자열 등의 단순 형식에 보낼 수 있습니다.

> [!NOTE]
> 단순 형식을 보내기 전에 대신 복합 형식의 값을 배치 하는 것이 좋습니다. 이 서버 쪽에서 모델 유효성 검사의 이점을 제공 하며, 쉽게 모델을 확장 하는 데 필요한 경우.


단순 형식을 전송 하는 기본 단계는 동일 하지만 두 가지 미묘한 차이점이 있습니다. 첫째, 컨트롤러에서 데코레이트해야 매개 변수 이름 앞에 **FromBody** 특성입니다.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

기본적으로 웹 API는 요청 URI에서에서 단순 형식을 가져오려고 시도 합니다. 합니다 **FromBody** 특성은 요청 본문에서 값을 읽을 수 있는 Web API에 알립니다.

> [!NOTE]
> 웹 API 응답 본문을 읽습니다 많아야 한 번만 매개 변수는 작업 중 하나는 요청 본문에서 가져올 수 있습니다. 요청 본문에서 여러 값을 얻으려면 해야 할 경우에 복합 형식을 정의 합니다.


둘째, 클라이언트는 다음 형식으로 값을 보낼 필요 합니다.

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

특히, 이름/값 쌍의 이름 부분을 단순 형식에 대 한 비어 있어야 합니다. 일부 브라우저는이 HTML 폼에 대 한 지원 하지만 다음과 같이 스크립트에서이 형식의 만듭니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

폼에는 예제는 다음과 같습니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

및 양식 값을 제출 하는 스크립트 다음과 같습니다. 이전 스크립트에서 유일한 차이점은에 전달 된 인수를 **게시물** 함수입니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

단순 형식의 배열을 보낼 동일한 접근 방식을 사용할 수 있습니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>추가 리소스

[2 부: 파일 업로드 및 다중 파트 MIME](sending-html-form-data-part-2.md)
