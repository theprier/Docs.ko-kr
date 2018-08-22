---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET 클라이언트 (C#)에서 Web API 호출 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 11/24/2017
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: be237bee43bc5e32939cb0b3e0948fd8b35bd1eb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832311"
---
<a name="call-a-web-api-from-a-net-client-c"></a>.NET 클라이언트 (C#)에서 Web API 호출
====================
하 여 [Mike Wasson](https://github.com/MikeWasson) 고 [Rick Anderson](https://twitter.com/RickAndMSFT)

[완료 된 프로젝트 다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)합니다. [지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample). 

이 자습서에서는.NET 응용 프로그램, web API를 호출 하는 방법을 보여 줍니다.를 사용 하 여 [System.Net.Http.HttpClient 합니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

이 자습서에서는 다음 웹 API를 사용 하는 클라이언트 앱을 작성 됩니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| 제품 ID 별로 가져오기 | 가져오기 | /api/products/*id* |
| 새 제품 만들기 | 올리기 | api 제품 |
| 제품 업데이트 | PUT | /api/products/*id* |
| 제품 삭제 | Delete | /api/products/*id* |

참조를 ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 [Web API에서는 CRUD 작업을 만드는](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)합니다.

간단히 하기 위해이 자습서에서는 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다. **HttpClient** Windows Phone 및 Windows 스토어 앱도 지원 됩니다. 자세한 내용은 참조 하세요. [여러 플랫폼 이식 가능한 라이브러리 사용에 대 한 웹 API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>콘솔 응용 프로그램 만들기

Visual Studio에서 명명 된 새 Windows 콘솔 앱을 만듭니다 **HttpClientSample** 다음 코드에 붙여 넣습니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

위의 코드는 전체 클라이언트 앱입니다.

`RunAsync` 실행 및 완료 될 때까지 차단 합니다. 대부분 **HttpClient** 메서드는 비동기, 네트워크 I/O를 수행 하는 때문에 있습니다. 내부에서 수행 하는 비동기 작업을 모두 `RunAsync`입니다. 일반적으로 앱 주 스레드를 차단 하지 않습니다 하지만이 앱이 모든 상호 작용을 허용 하지 않습니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>웹 API 클라이언트 라이브러리 설치

NuGet 패키지 관리자를 사용 하 여 웹 API 클라이언트 라이브러리 패키지를 설치 합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다. 에 콘솔 PMC (패키지 관리자), 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.Client`

위의 명령은 프로젝트에 다음 NuGet 패키지를 추가합니다.

* Microsoft.AspNet.WebApi.Client
* Newtonsoft.Json

Json.NET은.NET에 대 한 인기 있는 고성능 JSON 프레임 워크입니다.

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>모델 클래스 추가

검사는 `Product` 클래스:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

이 클래스는 웹 API에 의해 사용 되는 데이터 모델을 찾습니다. 앱에서 사용할 수 있습니다 **HttpClient** 읽을 수는 `Product` HTTP 응답 인스턴스입니다. 앱은 deserialization 코드를 작성할 필요가 없습니다.

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>만들기 및 HttpClient를 초기화 합니다.

정적 검사 **HttpClient** 속성:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient** 한 번 인스턴스화되면 되 고 응용 프로그램의 수명 내내 다시 사용 합니다. 다음 조건이 발생할 수 있습니다 **SocketException** 오류:

* 새로 만들 **HttpClient** 요청당 인스턴스.
* 부하가 서버입니다.

새로 만들 **HttpClient** 요청당 인스턴스는 사용 가능한 소켓 소모 될 수 있습니다.

다음 코드는 초기화 된 **HttpClient** 인스턴스:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

위의 코드:

* HTTP 요청에 대 한 기본 URI를 설정합니다. 서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다. 앱 서버 앱에 대 한 포트를 사용 하지 않으면 작동 하지 않습니다.
* Accept 헤더가 "application/json"으로 설정합니다. 이 헤더를 설정 합니다. JSON 형식으로 데이터를 보내도록 서버에 알려 줍니다.

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>리소스를 검색에 GET 요청을 보냄

다음 코드는 제품에 대 한 GET 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

합니다 **GetAsync** 메서드는 HTTP GET 요청을 보냅니다. 메서드가 완료 되 면 반환 된 **HttpResponseMessage** HTTP 응답을 포함 하는 합니다. 응답에 상태 코드가 성공 코드 인 경우 응답 본문에는 제품의 JSON 표현을 포함 합니다. 호출 **ReadAsAsync** JSON 페이로드를 deserialize 하는 데는 `Product` 인스턴스. 합니다 **ReadAsAsync** 메서드는 응답 본문은 임의로 큰 수 있기 때문에 비동기입니다.

**HttpClient** HTTP 응답 오류 코드를 포함 하는 경우 예외를 throw 하지 않습니다. 대신 합니다 **IsSuccessStatusCode** 속성은 **false** 상태가 오류 코드입니다. HTTP 오류 코드를 예외로 처리 하는 것을 선호 하는 경우 호출 [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 응답 개체입니다. `EnsureSuccessStatusCode` 상태 코드 200 범위를 벗어나는 경우 예외를 throw&ndash;299 합니다. 사실은 **HttpClient** 다른 이유로 예외를 throw 할 수 있습니다 &mdash; 예를 들어 요청 시간이 초과 됩니다.

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>Deserialize 하는 미디어 유형 포맷터

때 **ReadAsAsync** 라고 일련의 기본 매개 변수 없이 사용 *미디어 포맷터* 응답 본문을 읽을 수 있습니다. 기본 포맷터는 JSON, XML 및 양식 url로 인코딩된 데이터를 지원합니다.

기본 포맷터를 사용 하는 대신 하는 포맷터의 목록을 제공할 수 있습니다 합니다 **ReadAsAsync** 메서드.  포맷터 목록을 사용 하 여는 사용자 지정 미디어 유형 포맷터를 해야 하는 경우에 유용 합니다.

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

자세한 내용은 참조 하세요. [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md)

## <a name="sending-a-post-request-to-create-a-resource"></a>리소스를 만드는 POST 요청

다음 코드를 포함 하는 POST 요청이 전송 된 `Product` JSON 형식으로 인스턴스:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

합니다 **PostAsJsonAsync** 메서드:

* Json 개체를 serialize합니다.
* POST 요청에 JSON 페이로드를 보냅니다.

요청이 성공 합니다.

* 201 (만들어짐) 응답을 반환 해야 합니다.
* 응답의 Location 헤더의 생성된 된 리소스의 URL을 포함 해야 합니다.

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>리소스를 업데이트 하는 PUT 요청을 보내기

다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

합니다 **PutAsJsonAsync** 메서드처럼 작동 **PostAsJsonAsync**POST 대신 PUT 요청을 전송 하는 점을 제외 하 고, 합니다.

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>리소스를 삭제 하는 DELETE 요청을 보내기

다음 코드는 제품을 삭제 하는 DELETE 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

GET, 같은 삭제 요청 되지 않은 요청 본문입니다. 삭제를 사용 하 여 JSON 또는 XML 형식으로 지정할 필요가 없습니다.

## <a name="test-the-sample"></a>샘플 테스트

클라이언트 앱을 테스트 합니다.

1. [다운로드](https://github.com/aspnet/Docs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 및 서버 앱을 실행 합니다. [지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample). 서버 앱이 작동을 확인 합니다. Exaxmple에 대 한 `http://localhost:64195/api/products` 제품 목록을 반환 해야 합니다.
2. HTTP 요청에 대 한 기본 URI를 설정 합니다. 서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다.
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. 클라이언트 앱을 실행 합니다. 다음 출력이 생성됩니다.

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
