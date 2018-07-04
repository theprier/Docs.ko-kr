---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2에서에서 크로스-원본 요청을 사용 하도록 설정 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 크로스-원본 자원 공유 (CORS)를 지 원하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/15/2014
ms.topic: article
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 603eb55f8fa0b629d0287b66086b9495ef55faf7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381091"
---
<a name="enabling-cross-origin-requests-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 크로스-원본 요청을 사용 하도록 설정
====================
[Mike Wasson](https://github.com/MikeWasson)

> 브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다. 이 제약 사항을 *동일 원본 정책(Same-Origin Policy)* 이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다. 그러나 하려는 경우가 있습니다 수 다른 사이트에 web API를 호출할 수 있습니다.
> 
> [교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다. CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다. 이 자습서에는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013 업데이트 2](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - Web API 2.2


<a id="intro"></a>
## <a name="introduction"></a>소개

이 자습서에서는 ASP.NET Web API에서 CORS 지원 하는 방법을 보여 줍니다. 하나의 호출된 "웹 서비스", Web API 컨트롤러를 호스트 하는 다른 호출된 "WebClient", 웹 서비스를 호출 하는 두 개의 ASP.NET 프로젝트-만들어 시작 하겠습니다. 두 응용 프로그램은 서로 다른 도메인에서 호스트 되므로 WebService에 WebClient에서 AJAX 요청을 한 크로스-원본 요청이입니다.

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>"동일한 원본" 란?

두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

다음 두 URL은 동일한 원본입니다.

- `http://example.com/foo.html`
- `http://example.com/bar.html`

반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.

- `http://example.net` -도메인이 다릅니다
- `http://example.com:9000/foo.html` -포트가 다릅니다
- `https://example.com/foo.html` -스키마가 다릅니다
- `http://www.example.com/foo.html` -하위 도메인이 다릅니다

> [!NOTE]
> Internet Explorer 원본을 비교 하는 경우 포트를 고려 하지 않습니다.


<a id="create-webapi-project"></a>
## <a name="create-the-webservice-project"></a>웹 서비스 프로젝트를 만들려면

> [!NOTE]
> 이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 가정 합니다. 그렇지 않은 경우 [ASP.NET Web API를 사용 하 여 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.


Visual Studio를 시작 하 고 새 **ASP.NET 웹 응용 프로그램** 프로젝트입니다. 선택 된 **빈** 프로젝트 템플릿. "폴더를 추가 및 코어에 대 한 참조"를 선택 합니다 **Web API** 확인란을 선택 합니다. 필요에 따라 Mircosoft Azure에 앱을 배포 하는 "클라우드에서 호스트" 옵션을 선택 합니다. Microsoft에서 제공 하는 최대 10 개의 웹 사이트에 대해 무료 웹 호스트는 [무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

[![](enabling-cross-origin-requests-in-web-api/_static/image3.png)](enabling-cross-origin-requests-in-web-api/_static/image2.png)

명명 된 Web API 컨트롤러 추가 `TestController` 다음 코드를 사용 하 여:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

응용 프로그램을 로컬로 실행할 수도 있고 Azure에 배포할 수 있습니다. (이 자습서의 스크린샷에서, 필자 배포 Azure App Service Web Apps에.) Web API가 작동 하는지 확인 하려면로 이동 `http://hostname/api/test/`여기서 *호스트 이름* 응용 프로그램을 배포한 도메인입니다. 응답 텍스트가 &quot;가져오기: 테스트 메시지&quot;합니다.

![](enabling-cross-origin-requests-in-web-api/_static/image4.png)

<a id="create-client"></a>
## <a name="create-the-webclient-project"></a>WebClient 프로젝트를 만들려면

다른 ASP.NET 웹 응용 프로그램 프로젝트를 만들고 선택 합니다 **MVC** 프로젝트 템플릿. 필요에 따라 선택할 **인증 변경** > **인증 안 함**합니다. 이 자습서에 대 한 인증이 필요는 없습니다.

[![](enabling-cross-origin-requests-in-web-api/_static/image6.png)](enabling-cross-origin-requests-in-web-api/_static/image5.png)

솔루션 탐색기에서 Views/Home/Index.cshtml 파일을 엽니다. 이 파일의 코드를 다음으로 바꿉니다.

[!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

에 대 한 합니다 *serviceUrl* 변수를 웹 서비스 응용 프로그램의 URI를 사용 합니다. 이제 WebClient 앱을 로컬로 실행 하거나 다른 웹 사이트에 게시 합니다.

웹 서비스 앱에 나열 된 HTTP 메서드를 사용 하 여 AJAX 요청을 제출 "Try It" 단추를 클릭 하면 드롭다운 상자 (GET, POST 또는 PUT). 이 통해 다양 한 원본 간 요청을 검사할 수 있습니다. 현재, 웹 서비스 앱에 CORS를 지원 하지 않습니다 단추를 클릭 하면 오류가 발생할 수 있습니다.

![](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> 와 같은 도구에서 HTTP 트래픽을 시청 하는 경우 [Fiddler](http://www.telerik.com/fiddler)는 브라우저는 GET 요청을 보내지 및 요청이 성공 하지만 AJAX 호출이 오류를 반환 합니다. 표시 됩니다. 동일 원본 정책에서 브라우저 해도 알아야 할 것 *보내는* 요청 합니다. 대신 보지 못하도록 응용 프로그램을 방지 합니다 *응답*합니다.


![](enabling-cross-origin-requests-in-web-api/_static/image8.png)

<a id="enable-cors"></a>
## <a name="enable-cors"></a>CORS를 사용 하도록 설정

이제 웹 서비스 앱에서 CORS를 사용 하겠습니다. 첫째, CORS NuGet 패키지를 추가 합니다. Visual Studio에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

이 명령은 최신 패키지를 설치 하 고 core Web API 라이브러리를 포함 한 모든 종속성을 업데이트 합니다. 사용자-버전 플래그는 특정 버전을 대상으로 합니다. CORS 패키지에는 Web API 2.0 이상이 필요합니다.

앱 파일을 열고\_Start/WebApiConfig.cs 합니다. 다음 코드를 추가 합니다 **WebApiConfig.Register** 메서드.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

다음을 추가 합니다 **[EnableCors]** 특성을 `TestController` 클래스:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

에 대 한 합니다 *원본을* 매개 변수를 WebClient 응용 프로그램을 배포한 URI를 사용 합니다. 따라서 크로스-원본 요청에서 WebClient는 여전히 다른 모든 도메인 간 요청을 허용 하는 동안. 나중에 대 한 매개 변수를 설명할 **[EnableCors]** 자세히입니다.

끝에 슬래시를 포함 하지 않는 합니다 *원본을* URL입니다.

업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다. WebClient를 업데이트할 필요가 없습니다. 이제 WebClient에서 AJAX 요청이 성공 해야 합니다. GET, PUT 및 POST 메서드가 모두 허용 됩니다.

![](enabling-cross-origin-requests-in-web-api/_static/image9.png)

<a id="how-it-works"></a>
## <a name="how-cors-works"></a>CORS의 작동 원리

이 섹션에서는 HTTP 메시지 수준에서 CORS 요청에서 어떻게 설명 합니다. 구성할 수 있도록 CORS의 작동 방식을 이해 해야 합니다 **[EnableCors]** 올바르게 특성 및 예상 대로 작동 되지 않으면 문제를 해결 합니다.

CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다. 브라우저에서 CORS를 지 원하는 경우 크로스-원본 요청에 대해 자동으로 이러한 헤더 설정 모든 JavaScript 코드에 특별 한 작업을 수행할 필요가 없습니다.

크로스-원본 요청 예제는 다음과 같습니다. "원본" 헤더를 요청 하는 사이트의 도메인을 제공 합니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

서버 요청을 허용 하면, 액세스 제어-허용-원본 헤더를 설정 합니다. 이 헤더의 값 또는 원본 헤더와 일치 하는 와일드 카드 값 "\*", 즉 모든 원본을 허용 됩니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

응답에서 액세스 제어-허용-원본 헤더를 포함 하지 않습니다, AJAX 요청이 실패 합니다. 특히 브라우저 요청을 허용 하지 않습니다. 서버 응답에 성공 하면 반환 하는 경우에 브라우저 해도 응답 클라이언트 응용 프로그램에 사용할 수 있습니다.

**실행 전 요청**

브라우저는 일부 CORS 요청에 대 한 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청을" 라는 추가 요청을 보냅니다.

다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:

- 요청 메서드는 GET, HEAD 또는 POST *및*
- 응용 프로그램 동의 수용-언어 Content-language 이외의 모든 요청 헤더를 설정 하지 않습니다 Content-type, 또는 마지막-이벤트-ID *및*
- Content-type 헤더 (하는 경우 설정) 다음 중 하나입니다. 

    - application/x-www-form-urlencoded
    - 다중 파트/폼 데이터
    - 텍스트/일반

요청 헤더에 대 한 규칙을 호출 하 여 응용 프로그램을 설정 하는 헤더 적용할 **setRequestHeader** 에 **XMLHttpRequest** 개체입니다. (CORS 사양 이러한 "작성자 요청 헤더"를 호출 합니다.) 헤더에 규칙이 적용 되지 않습니다 합니다 *브라우저* 사용자 에이전트, 호스트 또는 콘텐츠-길이 같은 설정할 수 있습니다.

실행 전 요청의 예제는 다음과 같습니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다. 두 가지 특수 헤더를 포함합니다.

- 액세스-컨트롤-요청-방법: 실제 요청에 사용 될 HTTP 메서드.
- 요청 헤더 목록은 컨트롤-요청-헤더에 액세스 합니다:는 *응용 프로그램* 실제 요청을 설정 합니다. (마찬가지로이 브라우저 설정 하는 헤더)

예제 응답, 서버 요청을 허용 하는 다음과 같습니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

허용 된 메서드를 나열 하는 액세스-컨트롤-허용-메서드 헤더 및 필요에 따라 허용 되는 헤더를 나열 하는 액세스 제어-허용-헤더 헤더를 응답에 포함 됩니다. 실행 전 요청이 성공 하면 브라우저 앞에서 설명한 대로 실제 요청을 보냅니다.

<a id="scope"></a>
## <a name="scope-rules-for-enablecors"></a>[EnableCors]에 대 한 범위 규칙

응용 프로그램에서 작업당: 컨트롤러 당 또는 모든 Web API 컨트롤러에 대 한 전역적으로 CORS를 설정할 수 있습니다.

**작업당**

단일 작업에 대 한 CORS를 사용 하도록 설정 합니다 **[EnableCors]** 동작 메서드에 대 한 특성입니다. 다음 예제에서는 CORS는 `GetItem` 방법만 해당 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**컨트롤러당**

설정 하는 경우 **[EnableCors]** 컨트롤러 클래스에 대해 컨트롤러에서 모든 작업에 적용 합니다. CORS를 사용 하지 않으려면 작업을 추가 합니다 **[DisableCors]** 특성 작업을 합니다. 다음 예제에서는 제외한 모든 방법에 대 한 CORS를 사용 하면 `PutItem`합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**전 세계**

CORS를 사용 하도록 응용 프로그램에서 모든 Web API 컨트롤러에 대 한 전달를 **EnableCorsAttribute** 인스턴스를 **EnableCors** 메서드:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

둘 이상의 범위에서 특성을 설정 하는 경우 우선 순위가 같습니다.

1. 작업
2. 컨트롤러
3. Global

<a id="allowed-origins"></a>
## <a name="set-the-allowed-origins"></a>허용 되는 원본을 설정 합니다.

*원본을* 의 매개 변수를 **[EnableCors]** 특성 리소스에 액세스할 수 있는 원본 허용 되는지 지정 합니다. 값은 허용 되는 원본의 쉼표로 구분 된 목록.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

와일드 카드 값을 사용할 수도 있습니다 "\*" 요청을 모든 원본을 허용 하도록 합니다.

모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다. 말 그대로 모든 웹 사이트에 web API에 대 한 AJAX 호출을 설정할 수 있는지를 의미 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

<a id="allowed-methods"></a>
## <a name="set-the-allowed-http-methods"></a>허용 된 HTTP 메서드 설정

합니다 *메서드* 의 매개 변수를 **[EnableCors]** 리소스에 액세스할 수 있는 HTTP 메서드 특성 지정 합니다. 모든 메서드를 허용 하려면 와일드 카드 값을 사용 하 여 "\*"입니다. 다음 예제에서는 GET 및 POST 요청만 허용 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

<a id="allowed-request-headers"></a>
## <a name="set-the-allowed-request-headers"></a>허용 된 요청 헤더를 설정 합니다.

앞서 설명 했 듯이 실행 전 요청 액세스-컨트롤-요청-헤더 헤더를 포함할 수 있습니다 하는 방법을 나열 하는 응용 프로그램에 의해 설정 된 HTTP 헤더 (소위 "요청 헤더 author"). 합니다 *헤더* 의 매개 변수를 **[EnableCors]** 특성은 만든 요청 헤더를 허용 하도록 지정 합니다. 모든 헤더를 허용 하려면 설정 *헤더* 에 "\*"입니다. 허용 목록에 추가할 특정 헤더를 설정 *헤더* 허용 되는 헤더의 쉼표로 구분 된 목록에:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

그러나 브라우저에 대 한 액세스 제어-요청 헤더는 설정 하는 방법을 완전히 일치 하지 않습니다. 크롬이 "원본" 현재 포함 하는 예를 들어, 하지만 응용 프로그램이 스크립트를 설정 하는 경우에 FireFox "Accept"와 같은 표준 헤더를 포함 되지 않습니다.

설정 하는 경우 *헤더* 이외의 값으로 "\*"를 포함 해야 적어도 "수락", "콘텐츠-유형" 및 "원본"을 지원 하려는 모든 사용자 지정 헤더입니다.

<a id="allowed-response-headers"></a>
## <a name="set-the-allowed-response-headers"></a>허용 되는 응답 헤더 설정

기본적으로 브라우저 노출 하지 않습니다 모든 응용 프로그램에 대 한 응답 헤더입니다. 기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.

- 캐시 제어
- 콘텐츠 언어
- 콘텐츠 형식
- Expires
- Last-Modified
- Pragma

CORS 명세에서는 이 헤더들을 [단순 응답 헤더(Simple Response Header)](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header) 라고 부릅니다. 다른 헤더에서 응용 프로그램에 사용할 수 있도록 설정 합니다 *exposedHeaders* 의 매개 변수 **[EnableCors]** 합니다.

다음 예제에서는 컨트롤러의에서 `Get` 메서드 ' X 사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다. 기본적으로 브라우저는 크로스-원본 요청에서이 헤더를 노출 하지 않습니다. 헤더에서 사용할 수 있도록 하려면에 ' X 사용자 지정 헤더 '를 포함 *exposedHeaders*합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

<a id="credentials"></a>
## <a name="passing-credentials-in-cross-origin-requests"></a>크로스-원본 요청에 자격 증명 전달

CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다. 기본적으로 브라우저는 크로스-원본 요청을 사용 하 여 자격 증명을 보내지 않습니다. 여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다. 크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트 설정 해야 합니다 **XMLHttpRequest.withCredentials** true로 합니다.

사용 하 여 **XMLHttpRequest** 직접.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

jQuery를 사용할 경우:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

또한 서버에서도 자격 증명을 허용해야만 합니다. Web API에서 크로스-원본 자격 증명을 허용 하려면 설정 합니다 **SupportsCredentials** 속성에서 true로 합니다 **[EnableCors]** 특성:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

이 속성이 true 이면 HTTP 응답에 대 한 액세스 제어-허용-자격 증명 헤더가 포함 됩니다. 이 헤더는 서버를 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저를 알립니다.

브라우저에서 자격 증명을 보내는 응답을 유효한 액세스-컨트롤--자격 증명 허용 헤더를 포함 하지 않습니다 하지만 브라우저 응용 프로그램에 대 한 응답을 노출 하지 않습니다 고 AJAX 요청이 실패 합니다.

설정에 대 한 매우 주의 **SupportsCredentials** 다른 도메인에서 웹 사이트 사용자가 인식 하지 않고 사용자 대신 Web API에는 로그인 한 사용자의 자격 증명에 보낼 수 있기 때문에 true로 합니다. CORS 사양에는 또한 해당 설정 상태 *원본을* 에 &quot; \* &quot; 올바르지 경우 **SupportsCredentials** 그렇습니다.

<a id="cors-policy-providers"></a>
## <a name="custom-cors-policy-providers"></a>사용자 지정 CORS 정책 공급자

합니다 **[EnableCors]** 구현 특성을 **ICorsPolicyProvider** 인터페이스입니다. 파생 되는 클래스를 만들어 사용자 지정 구현을 제공할 수 있습니다 **특성** 구현 **ICorsProlicyProvider**합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

이제 배치 하는 위치 특성을 적용할 수 있습니다 **[EnableCors]** 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

예를 들어, 사용자 지정 CORS 정책 공급자를 구성 파일에서 설정을 읽을 수 없습니다.

특성을 사용 하는 대신,으로 등록할 수 있습니다는 **ICorsPolicyProviderFactory** 개체를 만드는 **ICorsPolicyProvider** 개체입니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

설정 하는 **ICorsPolicyProviderFactory**를 호출 합니다 **SetCorsPolicyProviderFactory** 같이 시작 시 확장 메서드:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

<a id="browser-support"></a>
## <a name="browser-support"></a>브라우저 지원

Web API CORS 패키지에는 서버 쪽 기술입니다. 사용자의 브라우저는 또한 CORS를 지원 해야 합니다. 다행 스럽게도 모든 주요 브라우저의 현재 버전 포함 [CORS에 대 한 지원](http://caniuse.com/cors)합니다.

Internet Explorer 8 및 Internet Explorer 9 부분에 대 한 지원이 CORS XMLHttpRequest 대신 레거시 XDomainRequest 개체를 사용 합니다. 자세한 내용은 [XDomainRequest-제한 사항, 제한 사항 및 해결 방법](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx)합니다.
