---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x 허브 API 가이드-JavaScript 클라이언트 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 허브 API를 사용 하 여 SignalR 브라우저 등 Windows 스토어 (WinJS) 합 JavaScript 클라이언트의 버전 1.1에 대 한 소개를 제공 하는 중...
ms.author: aspnetcontent
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 17b1088ca71f206e08bec62f3b13c43ad4bcc158
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828934"
---
<a name="signalr-1x-hubs-api-guide---javascript-client"></a>SignalR 1.x 허브 API 가이드-JavaScript 클라이언트
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

> 이 문서에서는 허브 API를 사용 하 여 SignalR 브라우저 (WinJS) Windows 스토어 응용 프로그램 등의 JavaScript 클라이언트의 버전 1.1에 대 한 소개를 제공 합니다.
> 
> SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.
> 
> 또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다. SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](../getting-started/index.md)합니다.


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [생성 된 프록시 및를 수행 하는 작업](#genproxy)

    - [생성 된 프록시를 사용 하는 경우](#cantusegenproxy)
- [클라이언트 설치](#clientsetup)

    - [동적으로 생성 된 프록시를 참조 하는 방법](#dynamicproxy)
    - [SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](#manualproxy)
- [연결을 설정 하는 방법](#establishconnection)

    - [$. connection.hub 동일 해당 $.hubConnection() 만듭니다 개체](#connequivalence)
    - [비동기 시작 메서드 실행](#asyncstart)
- [도메인 간 연결을 설정 하는 방법](#crossdomain)
- [연결을 구성 하는 방법](#configureconnection)

    - [쿼리 문자열 매개 변수를 지정 하는 방법](#querystring)
    - [전송 메서드를 지정 하는 방법](#transport)
- [허브 클래스에 대 한 프록시를 가져오는 방법](#getproxy)
- [서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법](#callclient)
- [클라이언트에서 서버 메서드를 호출 하는 방법](#callserver)
- [연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)
- [오류를 처리 하는 방법](#handleerrors)
- [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법](#logging)

프로그래밍 하는 방법에 대 한 설명서에 대 한 서버 또는.NET 클라이언트는 다음 리소스를 참조 합니다.

- [SignalR 허브 API 가이드-서버](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR 허브 API 가이드-.NET 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)

.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크. .NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>생성 된 프록시 및를 수행 하는 작업

SignalR를 생성 하는 프록시 없이 SignalR service와 통신 하는 JavaScript 클라이언트를 프로그래밍할 수 있습니다. 용도 프록시에 연결 하 고 서버를 호출 하는 쓰기 메서드를 사용 하 여 서버에서 메서드를 호출 하는 코드의 구문을 간소화 됩니다.

생성된 된 프록시의 로컬 함수를 실행 중 이었던 것 처럼 보이는 구문을 사용할 수 있도록 하는 서버 메서드를 호출 하는 코드를 작성 하는 경우: 작성할 수 있습니다 `serverMethod(arg1, arg2)` 대신 `invoke('serverMethod', arg1, arg2)`합니다. 생성 된 프록시 구문을 서버 메서드 이름을 잘못 입력 하면 즉각적이 고 알아보기 쉬운 클라이언트 쪽 오류가 또한 수 있습니다. 및 서버 메서드를 호출 하는 코드를 작성 하기 위한 IntelliSense 지원의 가져올 수도 있습니다 프록시를 정의 하는 파일을 수동으로 만들어야 하는 경우.

예를 들어 서버에서 다음 허브 클래스를 있다고 가정 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

다음 코드 예제에서는 JavaScript 코드의 모양은 호출을 표시 합니다 `NewContosoChatMessage` 메서드 호출을 받는 서버에는 `addContosoChatMessageToPage` 서버에서 메서드.

**생성 된 프록시를 사용 하 여**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**생성 된 프록시 없이**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>생성 된 프록시를 사용 하는 경우

서버를 호출 하는 클라이언트 메서드에 대 한 여러 이벤트 처리기를 등록 하려는 경우 생성 된 프록시를 사용할 수 없습니다. 그렇지 않은 경우 생성 된 프록시를 사용 하도록 선택할 수 또는 코딩 기본 설정을 기반으로 하지. 사용 하지 않으려는 경우 "signalr /" URL에서 참조할 필요가 없습니다를 `script` 클라이언트 코드에서 요소입니다.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

JavaScript 클라이언트에 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요합니다. JQuery 버전 1.6.4 또는 1.7.2, 1.8.2, 1.9.1 등 주요 이상 버전 이어야 합니다. 생성 된 프록시를 사용 하려는 경우에 SignalR 생성 된 프록시 JavaScript 파일에 대 한 참조가 필요 합니다. 다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에 표시 될 수 있습니다 참조를 보여 줍니다.

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

이러한 참조를이 순서 대로 포함 되어야 합니다: jQuery, 그 후 SignalR core 및 SignalR 프록시 성입니다.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>동적으로 생성 된 프록시를 참조 하는 방법

앞의 예제에서는 SignalR 생성 된 프록시에 대 한 참조를 동적으로 생성 된 JavaScript 코드를 실제 파일에 없습니다. SignalR 즉석에서 프록시에 대 한 JavaScript 코드를 만들고 "/ signalr 허브" URL에 대 한 응답에서 클라이언트로 서비스를 제공 합니다. 서버에서 SignalR 연결에 대 한 다양 한 기본 URL을 지정한 경우에 `MapHubs` 메서드를 동적으로 생성 된 프록시 파일의 URL을 사용 하 여 사용자 지정 URL은 "/ hubs"를 추가 합니다.

> [!NOTE]
> Windows 8 (Windows 스토어) JavaScript 클라이언트에 대 한 동적으로 생성 된 것 대신 실제 프록시 파일을 사용 합니다. 자세한 내용은 [SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](#manualproxy) 이 항목의에서 뒷부분에 있습니다.


ASP.NET MVC 4 Razor 보기에서를 가리키는 데 프록시 파일 참조의 응용 프로그램 루트를 물결표를 사용 합니다.

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 4에서 SignalR을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)합니다.

ASP.NET MVC 3 Razor 보기에서 사용 하 여 `Url.Content` 프록시 파일 참조용:

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

ASP.NET Web Forms 응용 프로그램에서 사용 하 여 `ResolveClientUrl` 프록시 참조를 파일 또는 앱 루트 상대 경로 (물결표부터 시작)를 사용 하는 ScriptManager를 통해 등록 합니다.

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

일반적으로 CSS 또는 JavaScript 파일에 사용 하는 "/ signalr 허브" URL을 지정 하는 데 동일한 메서드를 사용 합니다. 물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 응용 프로그램은 제대로 작동 IIS Express를 사용 하 여 Visual Studio에서 테스트 해도 전체 IIS를 배포할 때 404 오류와 함께 실패 하는 경우. 자세한 내용은 **루트 수준 리소스에 대 한 참조 해결** 에서 [ASP.NET 웹 프로젝트에 대 한 Visual Studio에서 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx) MSDN 사이트입니다.

디버그 모드에서 Visual Studio 2012에서 웹 프로젝트를 실행 하 고 브라우저를 Internet Explorer를 사용 하는 경우에 프록시 파일을 볼 수 있습니다 **솔루션 탐색기** 아래에서 **스크립트 문서**에서처럼 합니다 다음 그림에서는 합니다.

![솔루션 탐색기에서 JavaScript 생성 된 프록시 파일](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

파일의 내용을 보려면, 두 번 클릭 **hubs**합니다. Visual Studio 2012 및 Internet Explorer를 사용 하지 않는 경우, 디버그 모드에서 없는 경우에 "/ signalR 허브" URL로 이동 하 여 파일의 콘텐츠를 가져올 수 있습니다. 예를 들어 사이트에서 실행 중인 `http://localhost:56699`으로 이동 하 여 `http://localhost:56699/SignalR/hubs` 브라우저에서 합니다.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성

동적으로 생성 된 프록시 또는 프록시 코드가 있는 물리적 파일을 만들 수 있으며 해당 파일을 참조할 키를 누릅니다. 에 대 한 캐싱 나 동작을 제어 하는 작업을 수행 하 또는 server 메서드 호출을 코딩 하는 경우 IntelliSense를 가져올 경우가 있습니다.

프록시 파일을 만들려면 다음 단계를 수행 합니다.

1. 설치 합니다 [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지.
2. 명령 프롬프트를 열고 이동 합니다 *도구* SignalR.exe 파일이 있는 폴더입니다. 다음 위치에서 도구 폴더는입니다.

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. 다음 명령을 입력합니다.

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    에 대 한 경로 *.dll* 일반적으로 *bin* 프로젝트 폴더의 폴더입니다.

    이 명령은 라는 파일을 만듭니다 *server.js* 와 같은 폴더에 *signalr.exe*합니다.
4. 배치 된 *server.js* 프로젝트에 적절 한 폴더에 파일, 응용 프로그램에 대해 적절 하 게 바꾸거나 및 "signalr /" 참조를 대신 참조를 추가 합니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정 하는 방법

연결을 설정 하기 전에 연결 개체를 만들고 프록시를 만들려면 서버에서 호출할 수 있는 방법에 대 한 이벤트 처리기를 등록 해야 합니다. 프록시 및 이벤트 처리기를 설정 하는 경우 호출 하 여 연결을 설정 합니다 `start` 메서드.

생성 된 프록시를 사용 하는 경우에 생성된 된 프록시 코드를 수행 하기 때문에 사용자 고유의 코드에서 연결 개체를 만들 필요가 없습니다.

<a id="nogenconnection"></a>

**연결 된 (생성된 된 프록시)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**생성된 된 프록시) (없음 연결**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다. 다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.

> [!NOTE]
> 호출 하기 전에 이벤트 처리기를 등록 하는 일반적으로 `start` 연결을 설정 하는 방법입니다. 연결을 설정한 후 몇 가지 이벤트 처리기를 등록 하려면를 수행할 수 있지만 호출 하기 전에 이벤트 처리기 중 하나 이상 등록 해야 하는 경우는 `start` 메서드. 그 이유 중 하나는 응용 프로그램에서 하는 많은 허브 있을 수 있지만 트리거 하려고 하는 `OnConnected` 그 중 하나를 사용 하 여만 하려는 경우 모든 허브에 이벤트입니다. 연결이 설정 되 면 클라이언트에 대 한 메서드는 허브 프록시는 어떤 지시를 트리거하는 SignalR을 `OnConnected` 이벤트입니다. 호출 하기 전에 이벤트 처리기를 등록 하지 않으면 합니다 `start` 허브에 있지만 허브의 메서드를 호출할 수 있는 메서드를 `OnConnected` 메서드를 호출할 수 없습니다 하 고 서버에서 클라이언트 메서드가 호출 됩니다.


<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. connection.hub 동일 해당 $.hubConnection() 만듭니다 개체

알 수 있듯이 예제에서는에서 생성 된 프록시를 사용 하는 경우 `$.connection.hub` 연결 개체를 가리킵니다. 이 동일한 개체를 호출 하 여 가져올 `$.hubConnection()` 생성 된 프록시를 사용 하지 않는 경우. 생성된 된 프록시 코드는 다음 문을 실행 하 여 연결을 만듭니다.

![생성된 된 프록시 파일에서 연결 만들기](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

생성 된 프록시를 사용 하는 작업을 수행할 수 있습니다 `$.connection.hub` 생성 된 프록시를 사용 하지 않는 경우 연결 개체를 사용 하 여 수행할 수 있습니다.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>비동기 시작 메서드 실행

`start` 메서드를 비동기적으로 실행 합니다. 반환을 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/), 즉, 같은 메서드를 호출 하 여 콜백 함수를 추가할 수 있습니다 `pipe`를 `done`, 및 `fail`합니다. 연결이 설정 된 후에 실행 하려는 코드가 있는 경우에 서버 메서드 호출을 같은 콜백 함수에 해당 코드를 입력 하거나 콜백 함수에서 호출 합니다. `.done` 연결을 설정한 후에 모든 코드가 후 콜백 메서드가 실행 되기에 `OnConnected` 서버의 이벤트 처리기 메서드 실행을 완료 합니다.

뒤에 코드의 다음 줄으로 앞의 예제에서 "이제 연결" 문을 넣으면 합니다 `start` 메서드 호출 (아닌를 `.done` 콜백), `console.log` 다음과에서 같이 줄 연결 되기 전에 실행 합니다 예:

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>도메인 간 연결을 설정 하는 방법

일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에 `http://contoso.com/signalr`입니다. 경우 페이지가 `http://contoso.com` 에 연결 `http://fabrikam.com/signalr`, 도메인 간 연결입니다. 보안상의 이유로 기본적으로 도메인 간 연결을 사용할 수 있습니다. 도메인 간 연결을 설정 하려면 서버에서 도메인 간 연결이 설정 되어 있는지 확인 하 고 연결 개체를 만들 때 연결 URL을 지정 합니다. SignalR과 같은 적절 한 기술을 도메인 간 연결에 대 한 사용 됩니다 [JSONP](http://en.wikipedia.org/wiki/JSONP) 하거나 [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)합니다.

서버에서 호출 하는 경우 해당 옵션을 선택 하 여 도메인 간 연결을 설정 합니다 `MapHubs` 메서드.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

클라이언트에서 생성된 된 프록시) (없음 연결 개체를 만들 때나 (사용 하 여 생성된 된 프록시) 시작 메서드를 호출 하기 전에 URL을 지정 합니다.

**도메인 간 연결 (사용 하 여 생성된 된 프록시)를 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

**생성된 된 프록시) (없이 도메인 간 연결을 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

사용 하는 경우는 `$.hubConnection` 포함할 필요가 생성자 `signalr` URL에 자동으로 추가 되므로 (지정 하지 않으면 `useDefaultUrl` 으로 `false`).

다른 끝점으로 여러 연결을 만들 수 있습니다.

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - 설정 하지 않은 `jQuery.support.cors` 코드에서 true로 합니다.
> 
>     ![JQuery.support.cors true로 설정 하지](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     SignalR 처리 JSONP 또는 CORS를 사용 합니다. 설정 `jQuery.support.cors` true SignalR를 브라우저에서 CORS를 지원 하면 되므로 JSONP 사용 하지 않도록 설정 하려면.
> - Localhost URL에 연결할 때 Internet Explorer 10 않습니다 고려 도메인 간 연결을 응용 프로그램은 작동 로컬로 IE 10을 사용 하 여 서버에서 도메인 간 연결을 설정 하지 않은 경우에 합니다.
> - Internet Explorer 9를 사용 하 여 도메인 간 연결을 사용 하는 방법에 대 한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)합니다.
> - Chrome을 사용 하 여 도메인 간 연결을 사용 하는 방법에 대 한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)합니다.
> - 기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다. 다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.


<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성 하는 방법

연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정할 수도 있고 전송 방법을 지정할 수 있습니다.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정 하는 방법

클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.

**(사용 하 여 생성된 된 프록시) 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

**(없이 생성된 된 프록시) 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 메서드를 지정 하는 방법

연결 하는 프로세스의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 확인 하도록 서버를 사용 하 여 협상 합니다. 사용 하려는 하는 전송을 알고 있는 경우 호출 하는 경우에 전송 메서드를 지정 하 여이 협상 프로세스를 무시할 수 있습니다는 `start` 메서드.

**생성된 된 프록시) (사용 하 여 전송 메서드를 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**생성된 된 프록시) (없이 전송 메서드를 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

대신 시도 하는 SignalR 하려는 순서로 여러 전송 메서드를 지정할 수 있습니다.

**(사용 하 여 생성된 된 프록시) 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

**(하지 않는 생성된 된 프록시) 사용자 지정 전송 대체 (fallback) 스키마를 지정 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

전송 메서드를 지정 하기 위한 다음 값을 사용할 수 있습니다.

- "webSockets"
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

다음 예제에서는 연결에서 사용 중인 전송 방법을 확인 하는 방법을 보여 줍니다.

**(생성된 된 프록시)와 연결을 사용한 전송 메서드를 표시 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

**(없이 생성된 된 프록시) 연결에서 사용 하는 전송 메서드를 표시 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

서버 코드에서 전송 메서드를 확인 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법을](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)합니다. 전송 및 대체에 대 한 자세한 내용은 참조 하세요. [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>허브 클래스에 대 한 프록시를 가져오는 방법

사용자가 만든 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 대 한 연결에 대 한 정보를 캡슐화 합니다. 허브 클래스와 통신 하려면 사용자가 직접 만든 (생성 된 프록시를 사용 하지 않는) 하는 경우는 또는를 생성 되는 프록시 개체를 사용 합니다.

클라이언트에서 프록시 이름을 카멜식 대 / 소문자의 버전이 허브 클래스 이름입니다. SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.

**서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조 가져오기**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

**허브 클래스 (없이 생성 된 프록시)에 대 한 클라이언트 프록시 생성**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

사용 하 여 허브 클래스를 데코 레이트 하는 경우는 `HubName` 특성, 대/소문자를 변경 하지 않고 이름을 정확 하 게 사용 합니다.

**HubName 특성을 사용 하 여 서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조 가져오기**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

**허브 클래스 (없이 생성 된 프록시)에 대 한 클라이언트 프록시 생성**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법

허브에서 서버를 호출할 수 있는 메서드를 정의 하려면 이벤트 처리기 허브 프록시를 사용 하 여 추가 합니다 `client` 생성 된 프록시 또는 호출의 속성을 `on` 메서드 생성 된 프록시를 사용 하지 않는 경우. 매개 변수는 복잡 한 일 수 있습니다.

호출 하기 전에 이벤트 처리기를 추가 합니다 `start` 연결을 설정 하는 방법입니다. (호출한 후 이벤트 처리기를 추가 하려는 경우를 `start` 메서드를 참조 하십시오 [연결을 설정 하는 방법](#establishconnection) 앞부분에 나오는이 문서화 및 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 것에 대 한 표시 된 구문을 사용 하 여.)

메서드 이름 일치는 대/소문자 구분 합니다. 예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`를 `addContosoChatMessageToPage`, 또는 `addcontosochatmessagetopage` 클라이언트에서.

**(사용 하 여 생성된 된 프록시) 클라이언트에서 메서드를 정의 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

**(사용 하 여 생성된 된 프록시) 클라이언트에서 메서드를 정의 하는 대체 방법**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

**생성된 된 프록시 없이 등의 start 메서드를 호출한 후 추가 하는 경우 클라이언트에서 메서드를 정의 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

**클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

다음 예제에서는 메서드 매개 변수로 복잡 한 개체를 포함 합니다.

**복잡 한 개체 (사용 하 여 생성된 된 프록시)를 사용 하는 클라이언트에서 메서드를 정의 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

**생성된 된 프록시) (없이 복잡 한 개체를 사용 하는 클라이언트에서 메서드를 정의 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

**복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출 하는 방법

클라이언트에서 서버 메서드를 호출 하려면 사용 합니다 `server` 생성 된 프록시의 속성 또는 `invoke` 허브 프록시 생성 된 프록시를 사용 하지 않는 경우에 메서드. 반환 값 또는 매개 변수는 복잡 한 일 수 있습니다.

허브에서 카멜식 대 / 소문자 버전의 메서드 이름 전달 합니다. SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.

다음 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법 및 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.

**HubMethodName 특성이 없는 사용 하 여 서버 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

**매개 변수에 전달 된 복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

사용 하 여 허브 메서드를 데코 레이트 하는 경우는 `HubMethodName` 특성, 대/소문자를 변경 하지 않고 해당 이름을 사용 합니다.

**서버 메서드에서** HubMethodName 특성을 사용 하 여

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

앞의 예제에는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다. 다음 예제에서는 반환 값을 포함 하는 서버 메서드를 호출 하는 방법을 보여 줍니다.

**반환 값이 있는 메서드에 대 한 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

**사용 되는 Stock 클래스는** 값 반환

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리 하는 방법

SignalR 처리할 수 있는 수명 이벤트 다음 연결을 제공 합니다.

- `starting`: 데이터 연결을 통해 전송 되기 전에 발생 합니다.
- `received`: 연결에서 모든 데이터를 수신할 때 발생 합니다. 수신된 된 데이터를 제공합니다.
- `connectionSlow`: 클라이언트 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.
- `reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.
- `reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.
- `stateChanged`: 연결 상태가 변경 될 때 발생 합니다. 이전 상태 및 새 상태 (연결, 연결 됨, 다시 연결, 또는 Disconnected)를 제공합니다.
- `disconnected`: 연결이 끊어지면 발생 합니다.

예를 들어, 상당한 지연을 일으킬 수 있는 연결 문제가 있는 경우 경고 메시지를 표시 하려는 경우를 처리 합니다 `connectionSlow` 이벤트입니다.

**(사용 하 여 생성된 된 프록시) connectionSlow 이벤트를 처리 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

**생성된 된 프록시) (없이 connectionSlow 이벤트 처리**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](index.md)합니다.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류를 처리 하는 방법

SignalR JavaScript 클라이언트 제공는 `error` 이벤트에 대 한 처리기를 추가할 수 있습니다. 또한 server 메서드 호출에서 발생 하는 오류에 대 한 처리기를 추가 하려면 fail 메서드를 사용할 수 있습니다.

서버에 대 한 자세한 오류 메시지를 명시적으로 사용 하지 않는 경우 SignalR 오류가 발생 한 후 반환 하는 예외 개체는 오류에 대 한 최소한의 정보를 포함 합니다. 예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패 하면 오류 개체에 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 프로덕션에서 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려는 경우 있지만 보안상의 이유로 적합 하지 않습니다 보내기 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.

**(사용 하 여 생성된 된 프록시) 오류 처리기를 추가 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

**오류 처리기 (없이 생성된 된 프록시)를 추가 합니다.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.

**(사용 하 여 생성된 된 프록시) 메서드 호출에서 오류 처리**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

**생성된 된 프록시) (없이 메서드 호출에서 오류 처리**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

메서드 호출에 실패 하면를 `error` 이벤트도 발생 하므로에서 코드를 `error` 메서드 처리기 및는 `.fail` 메서드 콜백이 실행 됩니다.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법

클라이언트 쪽에서 로깅을 사용 하도록 연결을 설정 합니다 `logging` 를 호출 하기 전에 연결 개체의 속성을 `start` 연결을 설정 하는 방법.

**(사용 하 여 생성된 된 프록시) 로깅을 사용 하도록 설정**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

**(없이 생성된 된 프록시) 로깅을 사용 하도록 설정**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

로그를 확인 하려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여주는 스크린샷 단계별 지침 및 화면을 보여 주는 자습서를 참조 하세요 [로깅을 사용 하도록 설정-ASP.NET Signalr을 사용 하 여 서버 브로드캐스트](index.md)합니다.
