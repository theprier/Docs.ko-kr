---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c1c85f462141daf747e23aa4215d47f2d263140
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386710"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API에서에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME
====================
[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>2 부: 파일 업로드 및 다중 파트 MIME

이 자습서에는 웹 API에 파일을 업로드 하는 방법을 보여 줍니다. 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.

> [!NOTE]
> [완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.


파일을 업로드 하는 것에 대 한 HTML 폼의 예는 다음과 같습니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

이 양식에 텍스트 입력된 컨트롤 및 파일 입력된 컨트롤을 포함합니다. 폼 파일 입력된 컨트롤을 포함 하는 경우는 **enctype** 특성은 항상 &quot;다중 파트/폼 데이터&quot;, 다중 파트 MIME 메시지를 폼은 보내도록 지정 합니다.

예제 요청을 확인 하 여 이해 하기 쉬운 다중 파트 MIME 메시지의 형식은 다음과 같습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

이 메시지 두 나뉩니다 *파트*, 각각의 양식 컨트롤에 대 한 합니다. 부분 경계는 대시로 시작 하는 선으로 표시 됩니다.

> [!NOTE]
> 임의 구성 요소를 포함 하는 부분 경계 (&quot;41184676334&quot;) 경계 문자열 메시지 파트 내에서 실수로 표시 되지 않습니다 있도록 합니다.


각 메시지 파트 파트 콘텐츠에 뒤에 하나 이상의 헤더를 포함 합니다.

- Content-disposition 헤더 컨트롤의 이름을 포함합니다. 또한 파일에 대 한 파일 이름을 포함 합니다.
- Content-type 헤더에에서 데이터를 설명합니다. 이 헤더를 생략 하면 기본값은 텍스트/일반입니다.

이전 예제에서는 사용자 GrandCanyon.jpg, 콘텐츠 형식이 image/jpeg; 이라는 파일을 업로드 입력 텍스트의 값이 고 &quot;여름 휴가&quot;합니다.

## <a name="file-upload"></a>파일 업로드

이제는 다중 파트 MIME 메시지에서 파일을 읽는 Web API 컨트롤러에 살펴보겠습니다. 컨트롤러는 비동기적으로 파일을 읽이 됩니다. Web API를 사용 하 여 비동기 작업을 지원 합니다 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)합니다. 먼저, 다음은 코드를 지 원하는.NET Framework 4.5를 대상으로 하는 경우는 **비동기** 하 고 **await** 키워드입니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

알림 컨트롤러 작업 매개 변수를 사용 하지 않습니다. 미디어 유형 포맷터를 호출 하지 않고 작업 내에서 요청 본문을 처리 했습니다 때문입니다.

합니다 **IsMultipartContent** 메서드는 다중 파트 MIME 메시지를 요청에 포함 되는지 여부를 확인 합니다. 그렇지 않은 경우 컨트롤러 HTTP 상태 코드 415 (지원 되지 않는 미디어 형식)를 반환 합니다.

합니다 **MultipartFormDataStreamProvider** 클래스는 파일 스트림을 업로드 된 파일에 대 한 할당 하는 도우미 개체입니다. 다중 파트 MIME 메시지를 읽으려면 호출을 **ReadAsMultipartAsync** 메서드. 이 메서드는 모든 메시지 파트를 추출 하 고 제공한 스트림으로 씁니다 합니다 **MultipartFormDataStreamProvider**합니다.

메서드가 완료 되 면 파일에 대 한 정보를 가져올 수 있습니다 합니다 **데이터** 컬렉션인 속성의 **MultipartFileData** 개체입니다.

- **MultipartFileData.FileName** 저장 된 파일 서버의 로컬 파일 이름입니다.
- **MultipartFileData.Headers** 파트 헤더가 포함 되어 있습니다 (*하지* 요청 헤더). 콘텐츠에 액세스 하는 데 사용할 수 있습니다\_기질 및 Content-type 헤더입니다.

이름에서 알 수 있듯이 **ReadAsMultipartAsync** 비동기 메서드입니다. 메서드가 완료 된 후 작업을 수행 하려면 사용 된 [연속 작업이](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) 또는 **await** 키워드 (.NET 4.5).

.NET Framework 4.0 버전 이전 코드는 다음과 같습니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>양식 컨트롤 데이터 읽기

앞서 있는 HTML 폼에 텍스트 입력된 컨트롤을 했습니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

컨트롤의 값을 가져올 수는 **FormData** 의 속성을 **MultipartFormDataStreamProvider**합니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData** 되는 **NameValueCollection** 폼 컨트롤에 대 한 이름/값 쌍이 포함 된 합니다. 컬렉션 중복 키를 포함할 수 있습니다. 이 양식을 고려해 보세요.

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

요청 본문은 다음과 같습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

이런 경우는 **FormData** 컬렉션에는 다음 키/값 쌍을 포함 됩니다.

- 여정: 라운드트립
- 옵션: nonstop
- 옵션: 날짜
- 사용자: 창
