---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API의에서 HTML 폼 데이터 보내기: 파일 업로드 및 다중 파트 MIME | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 331d0e520a1fd8ec84aecd09a9c9e6d286c5893b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28040144"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API의에서 HTML 폼 데이터 보내기: 파일 업로드 및 다중 파트 MIME
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>2 단계: 파일 업로드 및 다중 파트 MIME

이 자습서에서는 웹 API에 파일을 업로드 하는 방법을 보여 줍니다. 또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.

> [!NOTE]
> [완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.


파일을 업로드 하는 것에 대 한 HTML 폼의 예는 다음과 같습니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

이 양식에 텍스트 입력된 컨트롤 및 파일 입력된 컨트롤을 포함합니다. 양식에 파일 입력된 컨트롤을 포함 하는 경우는 **enctype** 특성은 항상 &quot;multipart/폼 데이터&quot;, 폼으로 다중 파트 MIME 메시지를 보냈음을 지정 합니다.

예제 요청 확인 하 여 이해 하기 가장 쉽고 다중 파트 MIME 메시지의 형식은 다음과 같습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

이 메시지는 두 개의 나뉩니다 *부분*, 각 폼 컨트롤에 대 한 합니다. 일부가 경계는 대시로 시작 하는 선으로 표시 됩니다.

> [!NOTE]
> 임의의 구성 요소를 포함 하는 파트 경계 (&quot;41184676334&quot;)를 경계 문자열 메시지 파트 내 실수로 표시 되지 않습니다.


각 메시지 부분 파트 콘텐츠 앞에 오는 하나 이상의 머리글을 포함 합니다.

- Content-disposition 헤더 컨트롤의 이름을 포함합니다. 파일에 대 한 파일 이름을 포함 합니다.
- 콘텐츠 형식 헤더 데이터 부분에 설명합니다. 이 헤더를 생략 하면 기본값이 텍스트/일반입니다.

이전 예에서 사용자 콘텐츠 형식이 image/jpeg; GrandCanyon.jpg, 라는 파일을 업로드 입력 텍스트의 값은 &quot;여름 휴가&quot;합니다.

## <a name="file-upload"></a>파일 업로드

이제는 다중 파트 MIME 메시지에서 파일을 읽어 하는 Web API 컨트롤러에 살펴보겠습니다. 컨트롤러는 비동기적으로 파일을 읽이 됩니다. Web API를 사용 하 여 비동기 작업을 지 원하는 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)합니다. 먼저, 다음은 코드를 지 원하는.NET Framework 4.5를 대상으로 하는 경우는 **비동기** 및 **await** 키워드입니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

컨트롤러 동작 매개 변수를 사용 하지 않는 것을 확인 합니다. 미디어 유형 포맷터를 호출 하지 않고 작업을 내부 요청 본문 처리 때문입니다.

**IsMultipartContent** 메서드를 요청 하는 다중 파트 MIME 메시지에 포함 되어 있는지 여부를 확인 합니다. 그렇지 않으면 컨트롤러 HTTP 상태 코드 415 (지원 되지 않는 미디어 유형)을 반환 합니다.

**MultipartFormDataStreamProvider** 클래스는 파일 스트림을 업로드 된 파일에 할당 하는 도우미 개체입니다. 다중 파트 MIME 메시지를 읽으려면 호출는 **ReadAsMultipartAsync** 메서드. 이 메서드는 모든 메시지 파트를 추출 하 고에서 제공 하는 스트림을에 기록 된 **MultipartFormDataStreamProvider**합니다.

메서드가 완료 되 면에서 파일에 대 한 정보를 얻을 수 있습니다는 **데이터** 컬렉션인 속성의 **MultipartFileData** 개체입니다.

- **MultipartFileData.FileName** 저장 된 파일 서버에서 로컬 파일 이름입니다.
- **MultipartFileData.Headers** 파트 헤더가 포함 되어 (*하지* 요청 헤더). 콘텐츠에 액세스 하는 데 사용할 수 있습니다\_Disposition 및 콘텐츠 형식 헤더입니다.

이름에서 알 수 있듯이 **ReadAsMultipartAsync** 비동기 메서드입니다. 사용 하 여 파일을 메서드가 완료 된 후 작업을 수행 하는 [연속 작업](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) 또는 **await** 키워드 (.NET 4.5).

.NET Framework 4.0 버전의 이전 코드는 다음과 같습니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>양식 컨트롤 데이터 읽기

HTML 폼을 이전 보여 주었습니다 텍스트 입력된 컨트롤을 있습니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

컨트롤의 값을 얻을 수는 **FormData** 의 속성은 **MultipartFormDataStreamProvider**합니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData** 는 **NameValueCollection** 폼 컨트롤에 대 한 이름/값 쌍을 포함 하 합니다. 컬렉션에 중복 키가 포함 될 수 있습니다. 이 폼을 고려 합니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

요청 본문은 다음과 같이 표시 될 수 있습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

이 경우에 **FormData** 컬렉션 다음 키/값 쌍을 포함 합니다.

- 여행: 라운드트립
- 옵션: nonstop
- 옵션: 날짜
- 사용자 단위: 창
