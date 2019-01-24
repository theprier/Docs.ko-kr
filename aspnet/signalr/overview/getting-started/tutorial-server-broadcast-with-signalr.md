---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: tdykstra
description: 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: a243c78c7d552f1c82a88c6083871fcd16538618
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837431"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 브로드캐스트 서버

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트 서버가 클라이언트로 보낸 통신을 시작 하는 것을 의미 합니다.

이 자습서에서 만들어야 하는 응용 프로그램 주식 시세 표시기, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이션 합니다. 정기적으로 서버 임의로 주식 시세를 업데이트 및 모든 연결 된 클라이언트에 업데이트를 방송 합니다. 브라우저, 숫자 및 기호를 **변경** 하 고 **%** 열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다. 경우 모두 동일한 데이터 및 표시 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 엽니다.

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 프로젝트를 만듭니다.
> * 서버 코드 설정
> * 서버 코드를 검사 합니다.
> * 클라이언트 코드를 설정 하기
> * 클라이언트 코드를 검사 합니다.
> * 애플리케이션 테스트
> * 로깅 사용

> [!IMPORTANT]
> 응용 프로그램을 구축 하는 단계를 진행 하지 않으려는 경우에 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR.Sample 패키지를 설치할 수 있습니다. 이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하는 경우의 지침에 따라야 합니다 *readme.txt* 파일입니다. OWIN 시작을 추가 해야 패키지를 실행 하려면 호출 하는 클래스는 `ConfigureSignalR` 설치 패키지에는 메서드. OWIN startup 클래스를 추가 하지 않은 경우 오류를 받습니다. 참조 된 [StockTicker 샘플 설치](#install-the-stockticker-sample) 이 문서의 섹션입니다.


## <a name="prerequisites"></a>전제 조건

 * [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 에 **새 ASP.NET 웹 응용 프로그램-SignalR.StockTicker** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.

## <a name="set-up-the-server-code"></a>서버 코드 설정

이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-stock-class"></a>재고 클래스 만들기

만들어 시작 합니다 *재고* 모델 저장 하 고 주식에 대 한 정보를 전송 하는 데 사용할 수 있는 클래스입니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **클래스**합니다.

1. 클래스의 이름을 *재고* 하 고 프로젝트에 추가 합니다.

1. 코드를 대체 합니다 *Stock.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    주식을 만들 때 설정 하는 두 속성은 `Symbol` (예: microsoft MSFT) 및 `Price`합니다. 다른 속성을 설정 하는 방법 및 시기에 따라 달라 집니다 `Price`합니다. 처음 설정한 `Price`에 값을 가져옵니다 전파 `DayOpen`합니다. 그 후 설정한 경우 `Price`, 앱을 계산 합니다 `Change` 및 `PercentChange` 속성 값의 차이에 따라 `Price` 및 `DayOpen`.

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>StockTickerHub 및 StockTicker 클래스 만들기

서버와 클라이언트 간 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다. `StockTickerHub` 에서 파생 된 클래스는 `SignalRHub` 클래스 처리할 클라이언트에서 연결 및 메서드 호출을 수신 합니다. 주식 데이터를 유지 관리를 실행 해야는 `Timer` 개체입니다. `Timer` 개체는 주기적으로 클라이언트 연결의 독립적인 가격 업데이트를 트리거합니다. 이러한 함수 넣을 수 없습니다는 `Hub` 허브는 일시적인 클래스입니다. 앱을 만듭니다는 `Hub` 허브 연결 서버에 클라이언트에서 호출 등의 각 작업에 대 한 클래스 인스턴스. 따라서 주식 데이터를 유지 하 고, 가격을 업데이트, 브로드캐스트 가격 업데이트 하는 메커니즘은 별도 클래스에서 실행 해야 합니다. 클래스의 이름을 지정할 수 `StockTicker`입니다.

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-signalr/_static/image3.png)

원하는 인스턴스를 `StockTicker` 각 참조를 설정 해야 하므로 서버에서 실행 하는 클래스 `StockTickerHub` singleton 인스턴스 `StockTicker` 인스턴스. `StockTicker` 클래스는 주식 데이터 며 업데이트 트리거 하므로 클라이언트에 브로드캐스트 하지만 `StockTicker` 되지 않습니다는 `Hub` 클래스입니다. `StockTicker` 클래스에는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조를 가져오려고 합니다. SignalR 연결 컨텍스트 개체 다음 클라이언트로 브로드캐스트에 사용할 수 있습니다.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs 만들기

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-SignalR.StockTicker**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.

1. 클래스의 이름을 *StockTickerHub* 하 고 프로젝트에 추가 합니다.

    이 단계에서는 합니다 *StockTickerHub.cs* 클래스 파일입니다. 동시에 프로젝트에 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조의 집합을 추가 합니다.

1. 코드를 대체 합니다 *StockTickerHub.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 파일을 저장합니다.

앱에서는 합니다 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클라이언트는 서버에서 호출할 수 있습니다 하는 메서드를 정의 하는 클래스입니다. 한 가지 방법은 정의할: `GetAllStocks()`합니다. 처음에 클라이언트가 서버에 연결할 때 현재 가격을 사용 하 여 주식의 모든 목록을 가져오려면이 메서드를 호출 합니다. 메서드를 동기적으로 실행 반환 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문입니다.

메서드를 대기 데이터베이스 조회 또는 웹 서비스 호출 등을 포함 하는 것을 수행 하 여 데이터를 가져올 해야 하는 경우 지정 `Task<IEnumerable<Stock>>` 비동기 처리를 사용 하도록 설정 하려면 반환 값으로. 자세한 내용은 [ASP.NET SignalR 허브 API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)합니다.

`HubName` 특성 앱 허브 클라이언트에서 JavaScript 코드에는 참조 하는 방법을 지정 합니다. 기본 클라이언트에서이 특성을 사용 하지 않으면 이름은 경우 클래스 이름의 camelCase 버전 `stockTickerHub`합니다.

나중에 볼 수 있듯이 만들면 합니다 `StockTicker` 클래스인 앱 해당 클래스의 singleton 인스턴스를 해당 정적에서 만듭니다 `Instance` 속성입니다. 단일 인스턴스의 `StockTicker` 얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 있습니다. 해당 인스턴스를 `GetAllStocks()` 메서드 사용 하 여 현재 주식 정보를 반환 합니다.

#### <a name="create-stocktickercs"></a>StockTicker.cs 만들기

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **클래스**합니다.

1. 클래스의 이름을 *StockTicker* 하 고 프로젝트에 추가 합니다.

1. 코드를 대체 합니다 *StockTicker.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

모든 스레드가 동일한 인스턴스의 StockTicker 코드를 실행 하 고는, 있으므로 StockTicker 클래스는 스레드로부터 안전 해야 합니다.

### <a name="examine-the-server-code"></a>서버 코드를 검사 합니다.

서버 코드를 검사 하 여 앱의 작동 원리를 이해 하는 데 도움이 됩니다.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>정적 필드의 singleton 인스턴스를 저장합니다.

코드를 정적 초기화 `_instance` 지 원하는 필드를 `Instance` 클래스의 인스턴스를 사용 하 여 속성입니다. 생성자는 private 이므로 앱을 만들 수 있는 클래스의 유일한 인스턴스인 것입니다. 앱 사용 [초기화 지연](/dotnet/framework/performance/lazy-initialization) 에 대 한는 `_instance` 필드입니다. 성능상의 이유로 것입니다. 인스턴스 만들기는 스레드로부터 안전 해야 하는 것입니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

클라이언트가 서버에 연결 될 때마다 별도 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스를 StockTicker singleton 인스턴스를 가져옵니다 합니다 `StockTicker.Instance` 정적 속성으로 앞에서 확인을 `StockTickerHub` 클래스입니다.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary 주식 데이터를 저장

생성자가 초기화 하는 `_stocks` 일부 예제 주식 데이터 컬렉션 및 `GetAllStocks` 주식을 반환 합니다. 이 컬렉션의 재고 반환한 앞서 살펴본 `StockTickerHub.GetAllStocks`에 서버 메서드는는 `Hub` 클라이언트가 호출할 수 있는 클래스입니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

주식 컬렉션으로 정의 되는 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 형식. 사용할 수 있습니다는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 명시적으로 변경 되도록 하는 경우 사전을 잠금.

이 샘플 응용 프로그램에 대 한 것이 확인 응용 프로그램 데이터를 메모리에 저장 하는 데 앱을 삭제 하는 경우 데이터가 손실 된 `StockTicker` 인스턴스. 실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 하 여 작업할 것입니다.

#### <a name="periodically-updating-stock-prices"></a>주식 시세를 정기적으로 업데이트 하는 중

생성자는 시작을 `Timer` 주기적으로 임의 기준 주식 시세를 업데이트 하는 메서드를 호출 하는 개체입니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer` 호출 `UpdateStockPrices`를 전달 하는 state 매개 변수에 null입니다. 앱에서 잠금을 사용 가격을 업데이트 하기 전에 `_updateStockPricesLock` 개체입니다. 코드에서는 다른 스레드를 가격을 업데이트 하 고 호출한 다음 `TryUpdateStockPrice` 목록의 각 주식에 있습니다. `TryUpdateStockPrice` 주가 변경할지 여부를 결정 하는 메서드 및 변경 하려면 얼마나 많은 합니다. 앱을 호출 하는 주가 변경 되 면 `BroadcastStockPrice` 브로드캐스트 모든 주가 변경 하려면 클라이언트를 연결 합니다.

`_updatingStockPrices` 지정 된 플래그 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 는 스레드로부터 안전 해야 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

실제 응용 프로그램에서는 `TryUpdateStockPrice` 메서드는 가격을 조회 하는 웹 서비스를 호출 합니다. 이 코드에서는 앱 난수 생성기를 사용 하 여 임의로 변경.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기

가격 변경 내용을 여기 발생 하기 때문에 합니다 `StockTicker` 개체를 호출 해야 하는 개체는 `updateStockPrice` 메서드 연결 된 모든 클라이언트를 합니다. 에 `Hub` 클래스는 API가 있다고 클라이언트 메서드를 호출 하지만 `StockTicker` 에서 파생 되지 합니다 `Hub` 클래스 고 대 한 참조를 `Hub` 개체. 연결 된 클라이언트에 브로드캐스트하는 `StockTicker` 클래스에는 SignalR 컨텍스트 인스턴스를 가져오려고는 `StockTickerHub` 클래스를 사용 하는 클라이언트에서 메서드를 호출 합니다.

생성자에 전달 참조 하는 단일 클래스 인스턴스를 만들 때 코드는 SignalR 컨텍스트에 대 한 참조를 가져옵니다 하 고 생성자에 배치 된 `Clients` 속성입니다.

두 가지 컨텍스트를 한 번만 가져올 하려는 이유: 컨텍스트 가져오기 이며 비용이 많이 드는 작업을 앱 설정 클라이언트에 전송 된 메시지의 의도 한 순서를 유지 한 후 시작 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

가져오기는 `Clients` 컨텍스트와 배치 속성을 `StockTickerClient` 속성이 있는 것 처럼 동일 하 게 표시 하는 메서드를 호출할 클라이언트 코드를 작성할 수 있습니다는 `Hub` 클래스. 예를 들어 모든 클라이언트에 브로드캐스트를 작성할 수 `Clients.All.updateStockPrice(stock)`입니다.

합니다 `updateStockPrice` 메서드를 호출 하는 `BroadcastStockPrice` 아직 존재 하지 않습니다. 클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다. 참조할 수 있습니다 `updateStockPrice` 여기 하므로 `Clients.All` 가 동적 이므로 앱 런타임에 식을 평가 합니다. 이 메서드 호출은 실행 되 면 SignalR 전송할 메서드 이름과 매개 변수 값을 클라이언트에 클라이언트 라는 메서드를 포함 하는 경우 `updateStockPrice`, 앱 메서드를 호출 하 고 매개 변수 값을 전달할 됩니다.

`Clients.All` 이면 모든 클라이언트에 보냅니다. SignalR은 클라이언트 또는 클라이언트에 보낼 그룹 지정을 다른 옵션을 제공 합니다. 자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버를 가로채 고 signalr 직접 URL을 알고 있어야 합니다. 이렇게 하려면 OWIN 시작 클래스를 추가 합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-SignalR.StockTicker** 선택 **설치 됨** > **시각적 C#**   >  **Web** 및 선택한 **OWIN Startup 클래스**합니다.

1. 클래스의 이름을 *시동* 선택한 **확인**합니다.

1. 기본 코드를 대체 합니다 *Startup.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

이제 서버 코드가 설정 작업이 완료 되었습니다. 다음 섹션에서는 클라이언트를 설정할 수 있습니다.

## <a name="set-up-the-client-code"></a>클라이언트 코드를 설정 하기

이 섹션에서는 클라이언트에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-html-page-and-javascript-file"></a>HTML 페이지 및 JavaScript 파일 만들기

HTML 페이지에 데이터가 표시 됩니다 및 JavaScript 파일에서 데이터를 구성 합니다.

#### <a name="create-stocktickerhtml"></a>StockTicker.html 만들기

먼저 HTML 클라이언트를 추가 합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.

1. 파일 이름을 *StockTicker* 선택한 **확인**합니다.

1. 기본 코드를 대체 합니다 *StockTicker.html* 이 코드를 사용 하 여 파일:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML 5 개의 열, 하나의 머리글 행 및 5 개 열에 모두 걸친 단일 셀을 사용 하 여 데이터 행을 사용 하 여 테이블을 만듭니다. 데이터 행 "로드 중..." 앱을 시작 하는 경우에 일시적으로 보여 줍니다. JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여 해당 내부 행에 추가 됩니다.

    스크립트 태그를 지정합니다.

    * JQuery 스크립트 파일입니다.

    * SignalR core 스크립트 파일입니다.

    * SignalR 프록시 스크립트 파일입니다.

    * 나중에 만드는 StockTicker 스크립트 파일입니다.

    앱은 SignalR 프록시 스크립트 파일을 동적으로 생성합니다. "/ Signalr 허브" URL을 지정 하 고에 대 한이 경우 허브 클래스에서 메서드에 대 한 프록시 메서드를 정의 `StockTickerHub.GetAllStocks`합니다. 원하는 경우 수동으로 생성할 수 있습니다이 JavaScript 파일을 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)합니다. 동적 파일 생성을 사용 하지 않도록 설정 해야 합니다 `MapHubs` 메서드를 호출 합니다.

1. **솔루션 탐색기**를 확장 하 고 **스크립트**합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자 SignalR 스크립트의 이후 버전이 설치 됩니다.

1. 프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 선택한 후 **시작 페이지로 설정**합니다.

#### <a name="create-stocktickerjs"></a>StockTicker.js 만들기

이제 JavaScript 파일을 만듭니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **JavaScript 파일**합니다.

1. 파일 이름을 *StockTicker* 선택한 **확인**합니다.

1. 이 코드를 추가 합니다 *StockTicker.js* 파일:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>클라이언트 코드를 검사 합니다.

클라이언트 코드를 검사 하 여 클라이언트 코드는 앱이 작동 하려면 서버 코드를 상호 작용 하는 방법을 배우는 데 도움이 됩니다.

#### <a name="starting-the-connection"></a>연결을 시작

`$.connection` SignalR 프록시를 가리킵니다. 코드에 대 한 프록시에 대 한 참조를 가져옵니다 합니다 `StockTickerHub` 클래스 넣습니다는 `ticker` 변수입니다. 설정 된 이름인 프록시 이름을 `HubName` 특성:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

파일의 코드의 마지막 줄을 SignalR을 호출 하 여 SignalR 연결을 초기화 하는 모든 변수 및 함수를 정의한 후 `start` 함수입니다. 합니다 `start` 비동기적으로 실행 하 고 반환 하는 함수를 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)합니다. 앱에는 비동기 작업을 완료 될 때 호출할 함수를 지정 하는 완료 함수를 호출할 수 있습니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>모든 스톡 가져오기

합니다 `init` 함수 호출을 `getAllStocks` 서버 기능에 재고 테이블을 업데이트 하려면 서버를 반환 하는 정보를 사용 하 합니다. 기본적으로 사용 해야 camelCasing 클라이언트에서 메서드 이름은 서버의 파스칼식도 확인할 수 있습니다. CamelCasing 규칙 메서드를 개체가 아닌에 적용 됩니다. 참조 하는 예를 들어 `stock.Symbol` 하 고 `stock.Price`가 아닌 `stock.symbol` 또는 `stock.price`합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

에 `init` 메서드 앱은 호출 하 여 서버에서 받은 각 주식 개체에 대 한 테이블 행에 대 한 HTML을 생성 `formatStock` 의 형식 속성에는 `stock` 개체를 호출 하 여 다음 `supplant` 합니다 의자리표시자를바꾸려면`rowTemplate` 변수는 `stock` 개체 속성 값입니다. 그런 다음 결과 HTML은 주식 테이블에 추가 됩니다.

> [!NOTE]
> 문의할 `init` 에 전달 하 여는 `callback` 비동기 이후에 실행 하는 함수 `start` 함수 완료 합니다. 호출 하면 `init` 호출한 후는 별도 JavaScript 문으로 `start`를 설정 하 고 연결을 완료 하는 시작 함수를 기다리지 않고 즉시 실행 함수를 오류가 발생 합니다. 이런 경우는 `init` 함수를 호출 하려고 합니다.는 `getAllStocks` 함수 앱 서버 연결을 설정 합니다.

#### <a name="getting-updated-stock-prices"></a>업데이트 된 주식 시세 가져오기

서버는 주식 가격을 변경 하는 경우 호출 하는 `updateStockPrice` 연결 된 클라이언트에서. 앱의 클라이언트 속성에 함수를 추가 합니다 `stockTicker` 사용할 수 있도록 호출을 서버에서 프록시입니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

합니다 `updateStockPrice` 함수 형식 테이블로 서버에서 받은 스톡 개체 행에서 동일한 방법으로 `init` 함수입니다. 테이블에 행을 추가 하는 대신이 클래스는 테이블에서 주식의 현재 행을 찾습니다을 새 행을 바꿉니다.

## <a name="test-the-application"></a>애플리케이션 테스트

확인 하기 위해 앱을 테스트할 수 작동 합니다. 주가 변동를 사용 하 여 라이브 재고 테이블을 표시 하는 모든 브라우저 창을 볼 수 있습니다.

1. 도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 앱을 실행 하려면 재생 단추를 선택 합니다.

    ![디버깅 모드 켜기 재생을 선택 하는 사용자의 스크린샷.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    표시 하는 브라우저 창이 열립니다는 **재고 테이블 Live**합니다. 주식은 처음에 줄을 표시 "로드 중...", 그런 다음 잠시 후 앱은 초기 주식 데이터 표시 및 변경 하는 주가 먼저 합니다.

1. 브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.

    처음 주식 표시 된 첫 번째 브라우저와 동일 하 고 변경 내용을 동시에 발생 합니다.

1. 모든 브라우저를 닫고 새 브라우저를 열고 동일한 URL로 이동 합니다.

    StockTicker singleton 개체 서버에서 실행을 계속 합니다. 합니다 **재고 테이블 Live** 주식 계속 해 서 변경에 함을 보여 줍니다. 그림 변경 0 사용 하 여 초기 표를 참조 하지 않습니다.

1. 브라우저를 닫습니다.

## <a name="enable-logging"></a>로깅 사용

SignalR 문제 해결에 도움이 되는 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수를 포함 합니다. 이 섹션에서는 로깅을 사용 하도록 설정 하 고 어떻게 로그를 알려 주는 다음 전송 방법 중 SignalR 사용 하 여 보여 주는 예제를 참조 하세요.

* [Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 최신 브라우저에서 지원 합니다.

* [서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), Internet Explorer 이외의 브라우저에서 지원 합니다.

* [프레임 영원히](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer에서 지원 합니다.

* [긴 폴링 Ajax](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.

지정된 된 연결에 대 한 SignalR 서버와 클라이언트 모두 지 원하는 최상의 전송 방법을 선택 합니다.

1. 오픈 *StockTicker.js*합니다.

1. 이 강조 표시 된 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. **F5** 키를 눌러 프로젝트를 실행합니다.

1. 브라우저의 개발자 도구 창을 열고 로그를 확인 하려면 콘솔을 선택 합니다. 새 연결 전송 방법을 협상 SignalR의 로그를 보려면 페이지를 새로 고침 해야 합니다.

    * Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 중인 경우 전송 메서드는 **Websocket**합니다.

    * Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 중인 경우 전송 메서드는 **iframe**합니다.

    * 전송 메서드는 Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 **Websocket**합니다.

        > [!TIP]
        > Firefox에서 Firebug 추가 기능을 콘솔 창을 얻기를 설치 합니다.

    * Firefox 19 (IIS 7.5) Windows 7을 실행 중인 경우 전송 메서드는 **서버에서 전송** 이벤트입니다.

## <a name="install-the-stockticker-sample"></a>StockTicker 샘플 설치

합니다 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker 응용 프로그램을 설치 합니다. NuGet 패키지를 처음부터 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다. 이 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 구현 하는 코드를 검토 합니다.

> [!IMPORTANT]
> 이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우에 프로젝트에 OWIN 시작 클래스를 추가 해야 합니다. NuGet 패키지의 readme.txt 파일에서는이 단계를 설명합니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR.Sample NuGet 패키지를 설치 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.

1. **NuGet 패키지 관리자: SignalR.StockTicker**을 선택 **찾아보기**합니다.

1. **패키지 소스**를 선택 **nuget.org**합니다.

1. 입력 *SignalR.Sample* 검색 상자에 선택 **Microsoft.AspNet.SignalR.Sample** > **설치**합니다.

1. **솔루션 탐색기**를 확장 합니다 *SignalR.Sample* 폴더입니다.

    폴더 및 해당 콘텐츠를 만든 SignalR.Sample 패키지를 설치 합니다.

1. 에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 선택한 후 **시작 페이지로 설정**합니다.

    > [!NOTE]
    > SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다에 있는 jQuery 버전은 프로그램 *스크립트* 폴더입니다. 새 *StockTicker.html* 패키지에서 설치 하는 파일을 *SignalR.Sample* 폴더 하지만 원래 실행하려는경우패키지를설치하는jQuery버전을사용하여동기화됩니다*StockTicker.html* 다시 파일, 스크립트 태그에서 jQuery 참조를 먼저 업데이트 해야 할 수 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

 첫 번째 앱에서 볼 수 있는 테이블에는 유용한 기능이 있었습니다. 전체 주식 시세 응용 프로그램이 새 기능을 보여 줍니다: 주식 증가 하 고 해당 색을 변경 하 고 주식 데이터를 표시 하는 가로 스크롤 창을 합니다.

1. **F5** 키를 눌러 앱을 실행합니다.

     처음으로 앱을 실행 하는 경우 "시장"는 "closed" 및 정적 테이블 및 되지 스크롤 하는 주식 종목 창을 표시 합니다.

1. 선택 **Open Market**합니다.

    ![실시간 주식 종목 스크린샷입니다.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **실시간 주식 시세 표시기** 가로로 스크롤할 수 상자 시작 하 고 서버 주기적으로 임의 기준 주가 변경 브로드캐스트를 시작 합니다.

    * 때마다 주가 변경, 앱 모두를 업데이트 합니다 **재고 테이블 Live** 및 **실시간 주식 시세 표시기**.

    * 주식의 가격 변동 양수 이면 앱 주식 면 녹색 배경을 표시 됩니다.

    * 변경이 음수 이면 앱에는 빨간색 배경의 주식 보여 줍니다.

1. 선택 **시장 닫습니다**합니다.

    * 테이블 업데이트 중지 합니다.

    * 전광판 스크롤이 중지 됩니다.

1. 선택 **재설정**합니다.

    * 모든 주식 데이터 다시 설정 됩니다.

    * 앱 가격 변경 내용 시작 하기 전에 초기 상태를 복원 합니다.

1. 브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.

1. 각 브라우저에서 동시에 동적으로 업데이트 하는 동일한 데이터가 표시 됩니다.

1. 컨트롤 중 하나를 선택 하면 모든 브라우저를 동시에 동일한 방식으로 응답 합니다.

### <a name="live-stock-ticker-display"></a>실시간 주식 시세 표시기 표시

합니다 **실시간 주식 시세 표시기** 표시 되는 순서가 지정 되지 않은 목록의 `<div>` CSS 스타일에서 요소를 단일 줄으로 형식이 지정 합니다. 앱 초기화 하 고 전광판 테이블과 동일한 방식으로 업데이트:의 자리 표시자를 대체 하 여는 `<li>` 템플릿 문자열을 동적으로 추가 합니다 `<li>` 요소를 사용 하는 `<ul>` 요소. JQuery를 사용 하 여 스크롤 포함 `animate` 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백 변경 하는 함수는 `<div>`합니다.

#### <a name="signalrsample-stocktickerhtml"></a>SignalR.Sample StockTicker.html

주식 시세 HTML 코드:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR.Sample StockTicker.css

주식 시세 CSS 코드:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR.Sample SignalR.StockTicker.js

이 jQuery 코드를 스크롤합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트를 호출할 수 있는 서버에서 추가 메서드

앱에 유연성을 추가할 추가 메서드는 앱에서 호출할 수 있습니다.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR.Sample StockTickerHub.cs

`StockTickerHub` 클래스는 클라이언트를 호출할 수 있는 네 가지 추가 메서드를 정의 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

앱 호출 `OpenMarket`, `CloseMarket`, 및 `Reset` 페이지의 맨 위에 있는 단추에 대 한 응답에서입니다. 모든 클라이언트에 즉시 전파 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다. 이러한 각 방법에서 메서드를 호출 합니다 `StockTicker` 클래스는 시장 상태 변경이 발생 한 다음 새 상태를 브로드캐스트합니다.

#### <a name="signalrsample-stocktickercs"></a>SignalR.Sample StockTicker.cs

에 `StockTicker` 클래스를 앱으로 시장의 상태를 유지 관리를 `MarketState` 반환 하는 속성을 `MarketState` 열거형 값:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

각 시장 상태를 변경 하는 방법 때문에 이와 같이 잠금 블록 안에 `StockTicker` 클래스를 스레드로부터 안전 해야 합니다.:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

이 코드는 스레드로부터 안전 해야 합니다 `_marketState` 지 원하는 필드를 `MarketState` 지정 된 속성 `volatile`:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

합니다 `BroadcastMarketStateChange` 및 `BroadcastMarketReset` 메서드는 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외에 이미 살펴보았습니다 BroadcastStockPrice 메서드 비슷합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버를 호출할 수 있는 클라이언트에서 추가 기능

합니다 `updateStockPrice` 함수는 이제 주식 종목 표시와 테이블을 모두 처리 하 고 사용 하 여 `jQuery.Color` 빨간색 및 녹색 깜빡입니다.

새 함수 *SignalR.StockTicker.js* 사용 하도록 설정 하 고 시장 상태에 따라 단추를 사용 하지 않도록 설정 합니다. 이러한도 중지 하거나 시작 합니다 **실시간 주식 시세 표시기** 가로 스크롤. 다양 한 함수에 추가 되는 때문 `ticker.client`, 앱에서는 합니다 [함수를 확장 하는 jQuery](http://api.jquery.com/jQuery.extend/) 추가할.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설정

클라이언트 연결을 설정, 후 일부 추가 작업을 수행에 있습니다.

* 시장 열림 또는 닫힘 적절 한 호출 하는 경우 찾기 `marketOpened` 또는 `marketClosed` 함수입니다.

* 단추에 대 한 server 메서드 호출을 연결 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

서버 메서드 앱 연결을 설정 후까지 단추 연결 되지 않습니다. 이므로 제공 되기 전에 코드는 서버 메서드를 호출할 수 없습니다.

## <a name="additional-resources"></a>추가 자료

이 자습서에서는 연결 된 모든 클라이언트에 게 서버에서 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다. 이제 모든 클라이언트에서 알림 응답에서 메시지를 정기적으로 브로드캐스트할 수 있습니다. 다중 스레드 singleton 인스턴스 개념이 멀티 플레이어 온라인 게임 시나리오에서 서버 상태를 유지 하기 위해 사용할 수 있습니다. 예를 들어 참조 [SignalR을 기반으로 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.

피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하세요. [Getting Started with SignalR](introduction-to-signalr.md) 하 고 [SignalR을 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)합니다.

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [ASP.NET SignalR](../../index.md)
* [SignalR 프로젝트](http://signalr.net/)
* [SignalR GitHub 및 샘플](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 프로젝트를 생성합니다.
> * 서버 코드 설정
> * 서버 코드를 검사합니다.
> * 클라이언트 코드를 설정 하기
> * 클라이언트 코드를 검사합니다.
> * 응용 프로그램 테스트
> * 활성화 된 로깅

ASP.NET SignalR 2를 사용 하 여 실시간 웹 응용 프로그램을 만드는 방법에 알아보려면 다음 문서로 계속 진행 하세요.
> [!div class="nextstepaction"]
> [SignalR을 사용 하 여 실시간 웹 앱 만들기](real-time-web-applications-with-signalr.md)