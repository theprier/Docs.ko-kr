---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 문서에서는 허브 API를 사용 하 여 버전 2 (WinRT) Windows 스토어, WPF, Silverlight 및 단점 같은.NET 클라이언트에서 SignalR에 대 한 소개를 제공 하는 중...
ms.author: riande
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 34356338f24788226351e8e22b47eaaf7ea03e61
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287985"
---
<a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (SignalR 1.x)
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 허브 API를 사용 하 여 버전 2 (WinRT) Windows 스토어, WPF, Silverlight 및 콘솔 응용 프로그램 등.NET 클라이언트에서 SignalR에 대 한 소개를 제공 합니다.
> 
> SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.
> 
> 또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다. SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](../getting-started/index.md)합니다.


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [클라이언트 설치](#clientsetup)
- [연결을 설정 하는 방법](#establishconnection)

    - [Silverlight 클라이언트에서 도메인 간 연결](#slcrossdomain)
- [연결을 구성 하는 방법](#configureconnection)

    - [WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법](#maxconnections)
    - [쿼리 문자열 매개 변수를 지정 하는 방법](#querystring)
    - [전송 메서드를 지정 하는 방법](#transport)
    - [HTTP 헤더를 지정 하는 방법](#httpheaders)
    - [클라이언트 인증서를 지정 하는 방법](#clientcertificate)
- [허브 프록시를 만드는 방법](#proxy)
- [서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법](#callclient)

    - [매개 변수 없이 메서드](#clientmethodswithoutparms)
    - [매개 변수 형식을 지정 하는 매개 변수를 사용 하 여 메서드](#clientmethodswithparmtypes)
    - [매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드](#clientmethodswithdynamparms)
    - [처리기를 제거 하는 방법](#removehandler)
- [클라이언트에서 서버 메서드를 호출 하는 방법](#callserver)
- [연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)
- [오류를 처리 하는 방법](#handleerrors)
- [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법](#logging)
- [WPF, Silverlight 및 콘솔 응용 프로그램 서버를 호출할 수 있는 클라이언트 방법에 대 한 샘플 코드](#wpfsl)

샘플.NET 클라이언트 프로젝트에 대 한 다음 리소스를 참조 합니다.

- [gustavo armenta / SignalR 샘플](https://github.com/gustavo-armenta/SignalR-Samples) github.com (WinRT, Silverlight, 콘솔 앱 예제).
- [DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) github.com (WPF 예제).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) github.com (콘솔 앱 예제).

프로그래밍 하는 방법에 대 한 설명서에 대 한 서버 또는 JavaScript 클라이언트는 다음 리소스를 참조 합니다.

- [SignalR 허브 API 가이드-서버](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR 허브 API 가이드-JavaScript 클라이언트](../guide-to-the-api/hubs-api-guide-javascript-client.md)

.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크. .NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

설치를 [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지 (되지 합니다 [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지). 이 패키지는.NET 4 및.NET 4.5에 대 한 WinRT, Silverlight, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원합니다.

버전의 SignalR 클라이언트에 있는 서버에 있는 버전과 다른 경우 SignalR은 차이 할 경우가 많습니다. 예를 들어, SignalR 2.0 버전은 출시을 설치 하는 서버의 경우 서버 1.1.x 2.0이 설치 되어 있는 클라이언트를 설치 되어 있는 클라이언트 지원 됩니다. 클라이언트 버전과 서버 버전 간의 차이점은 너무, SignalR throw는 `InvalidOperationException` 클라이언트 연결을 시도 하는 동안 예외가 발생 합니다. 오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"입니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정 하는 방법

만들 필요가 대 한 연결을 설정 하기 전에 `HubConnection` 개체 및 프록시를 만듭니다. 연결을 설정 하려면 호출을 `Start` 메서드는 `HubConnection` 개체입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> JavaScript 클라이언트에 대 한 하나 이상의 이벤트 처리기를 호출 하기 전에 등록 해야 합니다 `Start` 연결을 설정 하는 방법입니다. .NET 클라이언트에 대 한 필요한 아닙니다. JavaScript 클라이언트에 대 한 생성 된 프록시 코드를 자동으로 존재 하는 모든 허브에 대 한 프록시 서버에서 만들어지고 있는 허브를 표시 하는 방법에 처리기를 등록 클라이언트에서 사용 하려고 합니다. .NET 클라이언트에 대 한 수 있지만 만들 허브 프록시를 수동으로 SignalR를 사용 하 게 모든 허브에 대 한 프록시를 만드는 것으로 가정 하므로.


기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다. 다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.

`Start` 메서드를 비동기적으로 실행 합니다. 연결이 설정 되 면 코드의 다음 줄까지 실행 하지 않도록 확인을 사용 하 여 `await` ASP.NET 4.5 비동기 메서드에서 또는 `.Wait()` 동기 메서드에서. 사용 하지 않는 `.Wait()` WinRT 클라이언트에서.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

`HubConnection` 클래스는 스레드로부터 안전합니다.

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight 클라이언트에서 도메인 간 연결

Silverlight 클라이언트에서 도메인 간 연결을 사용 하는 방법에 대 한 정보를 참조 하세요 [는 서비스 사용 가능한 도메인 경계를 넘어 수행](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)합니다.

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성 하는 방법

연결을 설정 하기 전에 다음 옵션 중 하나를 지정할 수 있습니다.

- 동시 연결 수 제한 합니다.
- 쿼리 문자열 매개 변수입니다.
- 전송 메서드입니다.
- HTTP 헤더입니다.
- 클라이언트 인증서입니다.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법

WPF 클라이언트의 기본 값 2의 동시 연결의 최대 수를 증가 해야 합니다. 권장된 값은 10입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

자세한 내용은 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)합니다.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정 하는 방법

클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 메서드를 지정 하는 방법

연결 하는 프로세스의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 확인 하도록 서버를 사용 하 여 협상 합니다. 사용 하려는 하는 전송, 이미 알고 있는 경우에이 협상 프로세스를 무시할 수 있습니다. 전송 메서드를 지정 하려면 Start 메서드에 전송 개체에 전달 합니다. 다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

합니다 [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임 스페이스는 전송을 지정 하는 데 사용할 수 있는 다음 클래스를 포함 합니다.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (사용 가능 서버와 클라이언트 모두.NET 4.5를 사용 하는 경우에)
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (자동으로 선택 되는 클라이언트와 서버 모두에서 지원 되는 최상의 전송 합니다. 이 기본 전송입니다. 전달 하려면이 작업에 `Start` 메서드에 아무 것도 전달 하지 않고 것과 동일한 효과가 있습니다.)

브라우저에만 사용 되므로 ForeverFrame 전송이이 목록에 포함 되지 않습니다.

서버 코드에서 전송 메서드를 확인 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법을](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)합니다. 전송 및 대체에 대 한 자세한 내용은 참조 하세요. [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP 헤더를 지정 하는 방법

HTTP 헤더를 설정 하려면 사용 된 `Headers` 연결 개체의 속성입니다. 다음 예제에서는 HTTP 헤더를 추가 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>클라이언트 인증서를 지정 하는 방법

클라이언트 인증서를 추가 하려면 사용 된 `AddClientCertificate` 연결 개체에서 메서드.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>허브 프록시를 만드는 방법

허브를 서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하기 위해 및 서버에서 허브에서 메서드를 호출할 호출 하 여 허브에 대 한 프록시를 만들 `CreateHubProxy` 연결 개체에서. 문자열에 전달할 `CreateHubProxy` 허브 클래스의 이름 또는 지정 된 이름을 `HubName` 서버에서 사용 된 경우 특성입니다. 이름 일치는 대/소문자 구분 합니다.

**서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**허브 클래스에 대 한 클라이언트 프록시 생성**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

사용 하 여 허브 클래스를 데코 레이트 하는 경우는 `HubName` 특성에 해당 이름을 사용 합니다.

**서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**허브 클래스에 대 한 클라이언트 프록시 생성**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

프록시 개체는 스레드로부터 안전 합니다. 사실 호출 하는 경우 `HubConnection.CreateHubProxy` 여러 번 사용 하 여 동일한 `hubName`, 이와 같은 캐시 `IHubProxy` 개체입니다.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법

서버를 호출할 수 있는 메서드를 정의 하려면 프록시를 사용 하 여 `On` 이벤트 처리기를 등록 하는 방법입니다.

메서드 이름 일치는 대/소문자 구분 합니다. 예를 들어 `Clients.All.UpdateStockPrice` 서버에서 실행 됩니다 `updateStockPrice`를 `updatestockprice`, 또는 `UpdateStockPrice` 클라이언트에서.

여러 클라이언트 플랫폼에는 UI를 업데이트 하려면 메서드 코드를 작성 하는 방법에 대 한 다른 요구 사항이 있습니다. WinRT (Windows 스토어.NET) 클라이언트에 대 한 예로 나와 있습니다. WPF, Silverlight 및 콘솔 응용 프로그램 예제에 나와 [이 항목의 뒷부분에 나오는 별도 섹션](#wpfsl)합니다.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>매개 변수 없이 메서드

비 제네릭 오버 로드를 사용 하 여 처리 하는 메서드 매개 변수가 없으면는 `On` 메서드:

**매개 변수 없이 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**매개 변수 없이 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>형식 매개 변수를 지정 하는 매개 변수를 사용 하 여 메서드

처리 하는 메서드 매개 변수가 매개 변수의 형식을 제네릭 형식으로 지정 된 `On` 메서드. 제네릭 오버 로드가 있습니다를 `On` 메서드를 사용 하면 최대 8 개의 매개 변수 (Windows Phone 7에서 4)을 지정할 수 있습니다. 다음 예제에서는 매개 변수 하나에 전송 됩니다는 `UpdateStockPrice` 메서드.

**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**매개 변수에 대해 사용 되는 Stock 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**매개 변수를 사용 하 여 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드

제네릭 형식으로 매개 변수를 지정 하는 대 안으로 `On` 메서드를 동적 개체로 매개 변수를 지정할 수 있습니다.

**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**매개 변수에 대해 사용 되는 Stock 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>처리기를 제거 하는 방법

호출 처리기를 제거 하려면 해당 `Dispose` 메서드.

**서버에서 호출 된 메서드에 대 한 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**클라이언트 코드 처리기를 제거 하려면**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출 하는 방법

서버에서 메서드를 호출 하려면 사용는 `Invoke` 허브 프록시 메서드.

서버 메서드가 반환 값이 없는 경우의 비 제네릭 오버 로드를 사용 합니다 `Invoke` 메서드.

**반환 값이 없는 메서드에 대 한 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

서버 메서드 반환 값이 있으면 반환 형식을 제네릭 형식으로 지정 된 `Invoke` 메서드.

**반환 값 및 복합 형식 매개 변수를 사용 하는 메서드에 대 한 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**매개 변수 및 반환 값에 사용 되는 Stock 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**반환 값을 포함 하 고 ASP.NET 4.5 비동기 메서드를 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**반환 값을 포함 하 고 동기 메서드를 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

합니다 `Invoke` 비동기적으로 실행 하 고 반환 하는 메서드를 `Task` 개체입니다. 지정 하지 않으면 `await` 또는 `.Wait()`를 호출 하는 메서드 실행이 완료 되기 전에 코드의 다음 줄이 실행 됩니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리 하는 방법

SignalR 처리할 수 있는 수명 이벤트 다음 연결을 제공 합니다.

- `Received`: 연결에서 모든 데이터를 수신할 때 발생 합니다. 수신된 된 데이터를 제공합니다.
- `ConnectionSlow`: 클라이언트가 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.
- `Reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.
- `Reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.
- `StateChanged`: 연결 상태가 변경 될 때 발생 합니다. 이전 상태 및 새 상태를 제공합니다. 연결에 대 한 상태 값에 대해서 [ConnectionState 열거형](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)합니다.
- `Closed`: 연결이 끊어지면 발생 합니다.

예를 들어, 심각한 되지 않지만 간헐적인 연결 문제가 발생 하는 오류에 대 한 경고 메시지를 표시 하려는 경우 속도 저하 또는 자주 등 연결의 삭제를 처리 합니다 `ConnectionSlow` 이벤트입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류를 처리 하는 방법

서버에 대 한 자세한 오류 메시지를 명시적으로 사용 하지 않는 경우 SignalR 오류가 발생 한 후 반환 하는 예외 개체는 오류에 대 한 최소한의 정보를 포함 합니다. 예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패 하면 오류 개체에 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 프로덕션에서 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려는 경우 있지만 보안상의 이유로 적합 하지 않습니다 보내기 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR에서 발생 하는 오류를 처리 하려면에 대 한 처리기를 추가할 수 있습니다는 `Error` 연결 개체의 이벤트입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

메서드 호출에서 오류를 처리 하려면 try / catch 블록에서 코드를 래핑하십시오.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법

클라이언트 쪽 로깅을 사용 하려면 다음을 설정 합니다 `TraceLevel` 및 `TraceWriter` 연결 개체의 속성입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>WPF, Silverlight 및 콘솔 응용 프로그램 서버를 호출할 수 있는 클라이언트 방법에 대 한 샘플 코드

코드 샘플에서는 이전 서버를 호출할 수 있는 클라이언트 메서드를 정의 하는 것에 대 한 WinRT 클라이언트에 적용 됩니다. 다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당 하는 코드를 보여 줍니다.

### <a name="methods-without-parameters"></a>매개 변수 없이 메서드

**WPF 클라이언트 코드에서 서버 매개 변수 없이 호출 된 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Silverlight 클라이언트 코드에서 서버 매개 변수 없이 호출 된 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드에서 서버 매개 변수 없이 호출**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>형식 매개 변수를 지정 하는 매개 변수를 사용 하 여 메서드

**WPF 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출 된 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Silverlight 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출 된 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드

**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WPF 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Silverlight 클라이언트 코드는 동적 개체를 사용 하 여 매개 변수에 대해 매개 변수를 사용 하 여 서버에서 호출 된 메서드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드 호출**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
