---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2 사용 하 여 서버 브로드캐스트 한다 | Microsoft Docs'
author: tdykstra
description: 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트는 commun 의미 하는 중...
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: c2248e68b3c9411687ab6410f12ec85488fe0738
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837311"
---
<a name="tutorial-server-broadcast-with-signalr-2"></a>자습서: SignalR 2 사용 하 여 서버 브로드캐스트 한다
====================
하 여 [Tom Dykstra](https://github.com/tdykstra), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트 클라이언트로 전송 되는 통신 서버에서 시작 되는 것을 의미 합니다. 이 시나리오에는 클라이언트로 전송 되는 통신 클라이언트 중 하나 이상으로 시작 되는 채팅 응용 프로그램과 같은 피어-투-피어 시나리오 보다 다른 프로그래밍 접근 방법이 필요 합니다.
> 
> 이 자습서에서 만들어야 하는 응용 프로그램 주식 시세 표시기, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이션 합니다.
> 
> 이 항목에서는 Patrick Fletcher 하 여 원래 작성 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>이 자습서를 사용 하 여 Visual Studio 2012를 사용 하 여
> 
> 
> 이 자습서를 사용 하 여 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.
> 
> - 업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 최신 버전으로 합니다.
> - 설치 합니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.
> - 웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다. SignalR 클래스에 대 한 Visual Studio 템플릿 같은 설치 합니다 **허브**합니다.
> - 일부 템플릿 (와 같은 **OWIN 시작 클래스**)를 사용할 수 없습니다;이 대 한 클래스 파일을 대신 사용 합니다.
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

이 자습서에서는 주기적으로 "푸시" 하려는 실시간 응용 프로그램의 대표 하는 주식 시세 응용 프로그램을 만드는 하 또는 브로드캐스트, 연결 된 모든 클라이언트에 서버에서 알림. 이 자습서의 첫 번째 부분에서는 해당 응용 프로그램의 단순화 된 버전부터에서 만들어야 합니다. 자습서의 나머지 부분에서는 추가 기능을 포함 하는 NuGet 패키지를 설치 하 고 해당 기능에 대 한 코드를 검토 합니다.

이 자습서의 첫 번째 부분에서 빌드할 응용 프로그램 주식 데이터를 사용 하 여 표를 표시 합니다.

![StockTicker 초기 버전](tutorial-server-broadcast-with-signalr/_static/image1.png)

정기적으로 서버 임의로 주식 시세를 업데이트 하 고 모든 연결 된 클라이언트에 업데이트를 푸시합니다. 브라우저 숫자 및 기호에는 **변경** 하 고 **%** 열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다. 경우 모두 동일한 데이터 및 표시 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 엽니다.

이 자습서는 다음 섹션이 포함 되어 있습니다.

- [필수 조건](#prerequisites)
- [프로젝트를 만들려면](#createproject)
- [서버 코드 설정](#server)
- [클라이언트 코드를 설정 하기](#client)
- [응용 프로그램 테스트](#test)
- [로깅을 사용 하도록 설정](#enablelogging)
- [설치 하 고 전체 StockTicker 샘플을 검토 합니다.](#fullsample)
- [다음 단계](#nextsteps)

합니다 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지는 Visual Studio 프로젝트에 시뮬레이션 된 샘플 주식 시세 응용 프로그램을 설치 합니다.

> [!NOTE]
> 응용 프로그램을 구축 하는 단계를 진행 하지 않으려는 경우에 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR.Sample 패키지를 설치할 수 있습니다. 이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하면 **readme.txt 파일의 지침을 따라야**합니다. 패키지를 실행 하려면 설치 된 패키지에서 ConfigureSignalR 메서드를 호출 하는 OWIN 시작 클래스를 추가 해야 합니다. OWIN startup 클래스를 추가 하지 않은 경우 오류를 받습니다.


<a id="prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

시작 하기 전에 Visual Studio 2013이 컴퓨터에 설치 되어 있는지 확인 합니다. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2013 Express를 가져오려고 합니다.

<a id="createproject"></a>

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. **파일** 메뉴에서 클릭 **새 프로젝트**합니다.
2. 에 **새 프로젝트** 대화 상자에서 **C#** 아래에 있는 **템플릿** 선택한 **웹**합니다.
3. 선택 된 **ASP.NET 빈 웹 응용 프로그램** 서식 파일을 프로젝트의 이름 *SignalR.StockTicker*, 클릭 **확인**합니다.

    ![새 프로젝트 대화 상자](tutorial-server-broadcast-with-signalr/_static/image2.png)
4. 에 **새로 만들기 ASP.NET** 두십시오 프로젝트 창 **빈** 선택 하 고 클릭 **프로젝트 만들기**합니다.

    ![새 ASP 프로젝트 대화 상자](tutorial-server-broadcast-with-signalr/_static/image3.png)

<a id="server"></a>

## <a name="set-up-the-server-code"></a>서버 코드 설정

이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-stock-class"></a>재고 클래스 만들기

저장 하 고 주식에 대 한 정보를 전송 하는 데 사용할 수 있는 재고 모델 클래스를 만들어 시작 합니다.

1. 프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *Stock.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    주식을 만들 때 설정 하는 두 속성은 기호 (예: microsoft MSFT) 및 가격입니다. 다른 속성 가격을 설정 하는 방법 및 시기에 따라 달라 집니다. 처음 가격을 설정할 값을 가져옵니다 DayOpen에 전파 됩니다. 가격 및 DayOpen 간의 차이 기반으로 이후 시간 변경 가격을 설정 하면 시간과 PercentChange 속성 값이 계산 되 합니다.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>StockTicker 및 StockTickerHub 클래스 만들기

서버와 클라이언트 간 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다. SignalR 허브 클래스에서 파생 된 StockTickerHub 클래스는 클라이언트에서 연결 및 메서드 호출 수신을 처리 합니다. 또한 주식 데이터를 유지 관리 하 고 주기적으로 클라이언트 연결 독립적으로 가격 업데이트를 트리거하는 타이머 개체를 실행 해야 합니다. 허브 인스턴스는 일시적 이므로 허브 클래스에서 이러한 함수를 넣을 수 없습니다. 허브 클래스 인스턴스를 연결 및 서버에 클라이언트에서 호출 같은 허브에 대 한 각 작업에 대해 만들어집니다. 따라서는 주식 데이터를 유지 하 고, 가격을 업데이트, 가격 업데이트 브로드캐스트 메커니즘 StockTicker 이름을 지정할 수 있는 별도 클래스에서 실행 되어야 합니다.

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-signalr/_static/image5.png)

Singleton StockTicker 인스턴스에 대 한 참조를 각 StockTickerHub 인스턴스에서 설정 해야 하므로 서버에서 실행 하려면 StockTicker 클래스의 인스턴스가 하나씩만 사용할 수 있습니다. StockTicker 클래스는 주식 데이터 수 있고 업데이트를 트리거 아닌 StockTicker 허브 클래스 때문에 클라이언트에 브로드캐스트할 수 있게 해야 합니다. 따라서 StockTicker 클래스는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조 해야 합니다. SignalR 연결 컨텍스트 개체 다음 클라이언트로 브로드캐스트에 사용할 수 있습니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가 | SignalR 허브 클래스 (v2)** 합니다.
2. 새 허브의 이름을 *StockTickerHub.cs*를 클릭 하 고 **추가**합니다. SignalR NuGet 패키지를 프로젝트에 추가 됩니다.
3. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

    합니다 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스는 클라이언트가 서버에서 호출할 수는 메서드를 정의 하는 데 사용 됩니다. 하나의 메서드를 정의 하는: `GetAllStocks()`합니다. 처음에 클라이언트가 서버에 연결할 때 현재 가격을 사용 하 여 주식의 모든 목록을 가져오려면이 메서드를 호출 합니다. 메서드는 동기적으로 실행 하 고 반환할 수 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문입니다. 메서드를 대기 데이터베이스 조회 또는 웹 서비스 호출 등을 포함 하는 것을 수행 하 여 데이터를 가져올 해야 하는 경우 지정 `Task<IEnumerable<Stock>>` 비동기 처리를 사용 하도록 설정 하려면 반환 값으로. 자세한 내용은 [ASP.NET SignalR 허브 API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)합니다.

    HubName 특성 클라이언트에서 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다. 이 특성을 사용 하지 않는 경우 클라이언트의 기본 이름은 stockTickerHub 것이 경우 클래스 이름의 카멜식 대 / 소문자 버전입니다.

    알 수 있듯이 나중 StockTicker 클래스를 만들 때, 정적 인스턴스 속성에 해당 클래스의 singleton 인스턴스로 생성 됩니다. 얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 유지 됩니다 StockTicker의 singleton 인스턴스를 해당 인스턴스에 GetAllStocks 메서드는 현재 주식 정보를 반환 하는 데 사용 됩니다.
4. 프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *StockTicker.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

    여러 스레드가 동일한 인스턴스의 StockTicker 코드를 실행 하 고는, 있으므로 StockTicker 클래스는 threadsafe 여야 합니다.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>정적 필드의 singleton 인스턴스를 저장합니다.

    코드를 정적 초기화 \_클래스의이 인스턴스를 사용 하 여 인스턴스 속성을 지 원하는 인스턴스 필드 이므로 만들 수 있는 클래스의 유일한 인스턴스 생성자를 private로 표시 되어 있습니다. [초기화 지연](https://msdn.microsoft.com/library/dd997286.aspx) 에 사용 되는 \_없습니다 성능상의 이유로 인스턴스 생성 threadsafe 인지를 확인 하지만 인스턴스 필드입니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

    클라이언트가 서버에 연결 될 때마다 별도 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스를 StockTicker singleton 인스턴스를 가져옵니다 StockTicker.Instance 정적 속성에서 StockTickerHub 클래스 앞 부분에서 살펴본 대로 합니다.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary 주식 데이터를 저장

    생성자는 초기화는 \_주식 컬렉션은 몇 가지 샘플 주식 데이터와 GetAllStocks 주식을 반환 합니다. 앞서 살펴본 것 처럼이 컬렉션의 재고 StockTickerHub.GetAllStocks 클라이언트가 호출할 수 있는 허브 클래스에는 서버 메서드는에서 다시 반환 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

    주식 컬렉션으로 정의 되는 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 형식. 사용할 수 있습니다는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 명시적으로 변경 되도록 하는 경우 사전을 잠금.

    이 샘플 응용 프로그램에 대 한 것이 확인 응용 프로그램 데이터를 메모리에 저장 하는 데 StockTicker 인스턴스가 삭제 될 때 데이터가 손실 됩니다. 실제 응용 프로그램에서 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 하 여 작업할 것입니다.

    ### <a name="periodically-updating-stock-prices"></a>주식 시세를 정기적으로 업데이트 하는 중

    생성자를 주기적으로 임의 기준 주식 시세를 업데이트 하는 메서드를 호출 하는 타이머를 시작 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

    UpdateStockPrices는 state 매개 변수에 null을 전달 하는 타이머에서 호출 됩니다. 가격을 업데이트 하기 전에 잠금을에서 수행 되는 \_updateStockPricesLock 개체입니다. 코드를 다른 스레드를 가격을 업데이트 하 고 목록의 각 주식에 TryUpdateStockPrice 호출 다음을 확인 합니다. TryUpdateStockPrice 메서드 주가 변경할지 여부를 결정 및 변경 하려면 얼마나 많은 합니다. 주가 변경 되 면 모든 연결 된 클라이언트에 주식 가격 변동 브로드캐스트하 BroadcastStockPrice 라고 합니다.

    합니다 \_updatingStockPrices 플래그로 표시 됩니다 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 액세스할 threadsafe 인지 확인 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

    실제 응용 프로그램에서는 TryUpdateStockPrice 메서드; 가격을 조회 하는 웹 서비스 호출 이 코드에서 임의로 변경할 난수 생성기를 사용 합니다.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기

    가격이 변경 StockTicker 개체 여기 나오는, 때문에 연결 된 모든 클라이언트에서 updateStockPrice 메서드를 호출 해야 하는 개체입니다. 허브 클래스에서 클라이언트 메서드를 호출 하는 것에 대 한 API는 있지만 StockTicker 허브 클래스에서 파생 되지 않습니다 및 Hub 개체에 대 한 참조는 없습니다. 따라서 연결 된 클라이언트에 브로드캐스트를 위해 StockTicker 클래스를 StockTickerHub 클래스에 대 한 SignalR 컨텍스트 인스턴스를 가져오고 클라이언트에서 메서드를 호출 하는 데는 있습니다.

    생성자에 전달 참조 하는 단일 클래스 인스턴스를 만들 때 코드는 SignalR 컨텍스트에 대 한 참조를 가져옵니다 하 고 생성자 클라이언트 속성에 넣습니다.

    두 가지 컨텍스트를 한 번만 가져올 하려는 이유:은 비용이 많이 드는 작업 컨텍스트 가져오기 및 클라이언트에 전송 된 메시지의 의도 된 순서 유지는 하면 한 번 것입니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

    컨텍스트의 클라이언트 속성을 가져오고 StockTickerClient 속성에 배치 메서드를 호출할 클라이언트 허브 클래스에서와 동일 하 게 표시 하는 코드를 작성할 수 있습니다. 예를 들어 모든 클라이언트에 브로드캐스트 Clients.All.updateStockPrice(stock) 작성할 수 있습니다.

    BroadcastStockPrice를 호출 하는 updateStockPrice 메서드가 아직 존재 하지 않습니다. 클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다. Clients.All 런타임에 식을 평가할 즉 동적 이므로 여기 updateStockPrice를 참조할 수 있습니다. 이 메서드 호출은 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트 updateStockPrice 메서드가 있으면 해당 메서드가 호출 됩니다 및 매개 변수 값에 전달 됩니다.

    Clients.All 모든 클라이언트에 보내는 것을 의미 합니다. SignalR은 클라이언트 또는 클라이언트에 보낼 그룹 지정을 다른 옵션을 제공 합니다. 자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버를 가로채 고 signalr 직접 URL을 알고 있어야 합니다. 이렇게 하려면 OWIN 시작 클래스를 추가 합니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **추가 | OWIN 시작 클래스**합니다. 클래스의 이름을 **Startup.cs**합니다.
2. 코드를 바꿔 **Startup.cs** 다음을 사용 하 여 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

이제 서버 코드가 설정을 완료 했습니다. 다음 섹션에서 클라이언트를 설정할 수 있습니다.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>클라이언트 코드를 설정 하기

1. 프로젝트 폴더에 새 HTML 파일을 만들고 이름을 *StockTicker.html*합니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html)]

    HTML 5 개 열, 하나의 머리글 행 및 5 개 열에 모두 걸친 단일 셀을 사용 하 여 데이터 행을 사용 하 여 테이블을 만듭니다. 데이터 행 "로드 중..."를 표시 되 고 일시적으로 응용 프로그램을 시작 하는 경우에 표시 됩니다. JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여 해당 내부 행에 추가 됩니다.

    스크립트 태그는 jQuery 스크립트 파일, SignalR core 스크립트 파일, SignalR 프록시 스크립트 파일 및 나중에 만들 StockTicker 스크립트 파일을 지정 합니다. "/ Signalr 허브" URL을 지정 하는 SignalR 프록시 스크립트 파일을 동적으로 생성 및 StockTickerHub.GetAllStocks에 대 한이 경우 허브 클래스의 메서드에 대 한 프록시 메서드를 정의 합니다. 원하는 경우 수동으로 생성할 수 있습니다이 JavaScript 파일을 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) MapHubs 메서드 호출의 동적 파일 생성을 사용 하지 않도록 설정 합니다.
3. > [!IMPORTANT]
   > JavaScript 파일에 참조 하는지 확인 *StockTicker.html* 올바릅니다. 즉, jQuery 버전 스크립트 태그 (예에서 1.10.2)에서 프로젝트의 jQuery 버전과 동일 인지를 확인 *스크립트* 폴더, 스크립트 태그에서 SignalR 버전 SignalR 동일 인지 확인 하 고 프로젝트의 버전 *스크립트* 폴더입니다. 필요한 경우 스크립트 태그의 파일 이름을 변경 합니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 클릭 하 고 **시작 페이지로 설정**합니다.
5. 프로젝트 폴더에 새 JavaScript 파일을 만들고 이름을 *StockTicker.js*...
6. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

    $.connection SignalR 프록시를 가리킵니다. 코드는 StockTickerHub 클래스에 대 한 프록시에 대 한 참조를 가져오고 전광판 변수에 넣습니다. 프록시 이름은 [HubName] 특성으로 설정 된 이름:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

    모든 변수 및 함수를 정의한 후 파일의 코드의 마지막 줄 SignalR 시작 함수를 호출 하 여 SignalR 연결을 초기화 합니다. 시작 함수가 비동기적으로 실행 하 고 반환 된 [jQuery 지연 개체](http://api.jquery.com/category/deferred-object/), 비동기 작업이 완료 될 때 호출할 함수를 지정 하려면 완료 함수를 호출할 수 있다는 의미입니다...

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

    Init 함수 서버의 getAllStocks 함수를 호출 하 고 서버 재고 테이블을 업데이트 하려면 반환 된 정보를 사용 합니다. 기본적으로 사용 해야 카멜식 대/소문자 클라이언트에서 서버의 파스칼식 되어도 메서드 이름을 알 수 있습니다. 카멜식 대/소문자 규칙 메서드를 개체가 아닌에 적용 됩니다. 예를 들어, 재고를 참조할 수도 있습니다. 기호 및 stock 합니다. 가격, stock.symbol 않거나 stock.price 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

    클라이언트에서 파스칼식 대/소문자를 사용 하려는 경우 완전히 다른 메서드 이름을 사용 하려는 경우 있습니다 수 메서드를 데코레이팅합니다 허브 HubMethodName 특성을 사용 하 여 동일한 방식으로 HubName 특성을 사용 하 여 허브 클래스 자체 장식 합니다.

    Init 메서드에서 테이블 행에 대 한 HTML 주식 개체의 형식 속성을 호출 formatStock 하 여 서버에서 받은 각 주식 개체에 대해 생성 되 고 호출 하 여 다음 기능이 (맨 위에 있는 정의 된 *StockTicker.js*) 자리 표시자를 바꿔야 rowTemplate 변수에 주식 개체 속성 값을 사용 합니다. 그런 다음 결과 HTML은 주식 테이블에 추가 됩니다.

    비동기 시작 함수가 완료 된 후 실행 되는 콜백 함수에 전달 하 여 init를 호출 합니다. 시작을 호출한 후는 별도 JavaScript 문으로 init를 호출 하면 함수는 연결을 완료 하는 시작 함수를 기다리지 않고 즉시 실행 됩니다 때문에 실패 합니다. 이런 경우는 init 함수 서버 연결이 설정 되기 전에 getAllStocks 함수를 호출 하려고 합니다.

    서버는 주식 가격 변경 되 면 연결 된 클라이언트는 updateStockPrice 호출 합니다. 함수는 사용할 수 있도록 호출을 서버에서 stockTicker 프록시의 클라이언트 속성에 추가 됩니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

    UpdateStockPrice 함수는 init 함수와 동일 하 게 테이블 행에 서버에서 받은 주식 개체의 형식을 지정 합니다. 그러나 테이블에 행을 추가 하는 대신 주식의 현재 행에서 테이블을 찾아 새 행을 바꿉니다.

<a id="test"></a>

## <a name="test-the-application"></a>응용 프로그램 테스트

1. F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.

    주식은 처음에 "로드 중..." 줄을 다음 초기 주식 데이터를 표시 하는 짧은 지연 후 표시 하 고 변경 하는 주가 시작 하는 합니다.

    ![로드](tutorial-server-broadcast-with-signalr/_static/image6.png)

    ![초기 재고 테이블](tutorial-server-broadcast-with-signalr/_static/image7.png)

    ![서버에서 변경 내용을 수신할 주식 테이블](tutorial-server-broadcast-with-signalr/_static/image8.png)
2. 브라우저 주소 표시줄에서 URL을 복사 하 고 하나 이상의 새 브라우저 창에 붙여 넣습니다.

    처음 주식 표시 된 첫 번째 브라우저와 동일 하 고 변경 내용을 동시에 발생 합니다.
3. 모든 브라우저를 닫고 새 브라우저를 열고 하 고 동일한 URL로 이동 합니다.

    StockTicker singleton 개체 지속적 주식 테이블 표시를 변경 하는 주식 계속 해 서 서버에서 실행 하는 합니다. (그림 변경 0 사용 하 여 초기 표를 참조 하지 않습니다.)
4. 브라우저를 닫습니다.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>로깅 사용

SignalR 문제 해결에 도움이 되는 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수를 포함 합니다. 이 섹션에서는 로깅을 사용 하도록 설정 하 고 어떻게 로그를 알려 주는 다음 전송 방법 중 SignalR 사용 하 여 보여 주는 예제를 참조 하세요.

- [Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 최신 브라우저에서 지원 합니다.
- [서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), Internet Explorer 이외의 브라우저에서 지원 합니다.
- [프레임 영원히](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer에서 지원 합니다.
- [긴 폴링 Ajax](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.

지정된 된 연결에 대 한 SignalR 서버와 클라이언트 모두 지 원하는 최상의 전송 방법을 선택 합니다.

1. 오픈 *StockTicker.js* 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js)]
2. F5 키를 눌러 프로젝트를 실행합니다.
3. 브라우저의 개발자 도구 창을 열고 로그를 확인 하려면 콘솔을 선택 합니다. 새 연결 전송 방법을 협상 Signalr의 로그를 보려면 페이지를 새로 고침 해야 합니다.

    Windows 8 (IIS 8)에서 Internet Explorer 10를 실행 하는 경우 전송 방법은 Websocket입니다.

    ![IE 10 IIS 8 콘솔](tutorial-server-broadcast-with-signalr/_static/image9.png)

    Windows 7 (IIS 7.5)에서 Internet Explorer 10를 실행 하는 경우 전송 방법은 iframe입니다.

    ![IE 10 콘솔 IIS 7.5](tutorial-server-broadcast-with-signalr/_static/image10.png)

    Firefox에서 Firebug 추가 기능을 콘솔 창을 얻기를 설치 합니다. Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 Websocket입니다.

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-signalr/_static/image11.png)

    Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 이벤트가 서버에서 전송 합니다.

    ![Firefox 19 IIS 7.5 콘솔](tutorial-server-broadcast-with-signalr/_static/image12.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>설치 하 고 전체 StockTicker 샘플을 검토 합니다.

StockTicker 응용 프로그램으로 설치 되는 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지를 처음부터 방금 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다. 이 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 구현 하는 코드를 검토 합니다. 이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우에 프로젝트에 OWIN 시작 클래스를 추가 해야 합니다. 이 단계는 NuGet 패키지의 readme.txt 파일에 설명 되어 있습니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR.Sample NuGet 패키지를 설치 합니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.
2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **온라인**, 입력 *SignalR.Sample* 에 **온라인 검색** 상자를 선택한 다음 를클릭 **설치할** 에 **SignalR.Sample** 패키지 있습니다.

    ![SignalR.Sample 패키지 설치](tutorial-server-broadcast-with-signalr/_static/image13.png)
3. **솔루션 탐색기**를 확장 합니다 *SignalR.Sample* SignalR.Sample 패키지를 설치 하 여 생성 된 폴더입니다.
4. 에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 클릭 하 고 **시작 페이지로 설정**합니다.

    > [!NOTE]
    > SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다에 있는 jQuery 버전은 프로그램 *스크립트* 폴더입니다. 새 *StockTicker.html* 패키지에서 설치 하는 파일을 *SignalR.Sample* 폴더 하지만 원래 실행하려는경우패키지를설치하는jQuery버전을사용하여동기화됩니다*StockTicker.html* 다시 파일, 스크립트 태그에서 jQuery 참조를 먼저 업데이트 해야 할 수 있습니다.

### <a name="run-the-application"></a>응용 프로그램 실행

1. F5 키를 눌러 응용 프로그램을 실행합니다.

    앞서 살펴본는 그리드 외에도 전체 주식 시세 응용 프로그램에 동일한 주식 데이터를 표시 하는 가로 스크롤 창을 보여 줍니다. 처음으로 응용 프로그램을 실행 하면 "시장"는 "closed" 및 정적 표 및 되지 스크롤 하는 주식 종목 창을 표시 합니다.

    ![StockTicker 화면 시작](tutorial-server-broadcast-with-signalr/_static/image14.png)

    클릭 하면 **공개 시장**, **실시간 주식 시세 표시기** 가로로 스크롤할 수 상자 시작 하 고 서버 주기적으로 임의 기준 주가 변경 브로드캐스트를 시작 합니다. 주가 될 때마다 둘 다 변경 합니다 **재고 테이블 Live** 표 및 **실시간 주식 시세 표시기** 상자가 업데이트 됩니다. 주식의 가격 변동 양수 이면 주식 면 녹색 배경을 표시 됩니다 하 고 변경 하는 것이 음수 이면 주식 배경이 빨간색으로 표시 됩니다.

    ![StockTicker 앱 시장 열기](tutorial-server-broadcast-with-signalr/_static/image15.png)

    **닫기 시장** 변경을 중지 하 고 주식 종목 스크롤이 중지 하는 단추 및 **재설정** 가격 변경을 시작 하기 전에 단추를 초기 상태로 모든 주식 데이터를 초기화 합니다. 자세한 브라우저 창을 열고 동일한 URL로 이동 하는 경우 각 브라우저에서 동시에 동적으로 업데이트 하는 같은 데이터 표시 됩니다. 단추 중 하나를 클릭 하면 모든 브라우저를 동시에 동일한 방식으로 응답 합니다.

### <a name="live-stock-ticker-display"></a>실시간 주식 시세 표시기 표시

합니다 **실시간 주식 시세 표시기** 표시는 CSS 스타일으로 한 줄으로 포맷 된 div 요소에는 순서가 지정 되지 않은 목록입니다. 전광판 초기화 되 고 동일한 방식으로 테이블을 업데이트:의 자리 표시자를 대체 하 여를 &lt;li&gt; 템플릿 문자열을 동적으로 추가 합니다 &lt;li&gt; 요소를 사용 하는 &lt;ul&gt; 요소입니다. div. 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백 변경 하려면 jQuery 애니메이션 효과 주기 함수를 사용 하 여 수행 됩니다 스크롤

주식 시세 HTML:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

주식 시세 CSS:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

이 jQuery 코드를 스크롤합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트를 호출할 수 있는 서버에서 추가 메서드

StockTickerHub 클래스를 클라이언트가 호출할 수는 4 개의 추가 메서드를 정의 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

OpenMarket, CloseMarket, 및 재설정 페이지의 맨 위에 있는 단추에 대 한 응답으로 호출 됩니다. 모든 클라이언트에 즉시 전파 되는 상태의 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다. 이러한 메서드의 메서드를 호출 StockTicker 클래스에 해당 효과 시장 상태 변경 및 다음 새 상태를 브로드캐스트합니다.

StockTicker 클래스에서 시장 상태의 MarketState 열거형 값을 반환 하는 MarketState 속성으로 유지 됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

각 시장 상태를 변경 하는 방법 때문에 이와 같이 잠금 블록 안에 threadsafe 되도록 StockTicker 클래스에:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

이 코드는 threadsafe, 확인 된 \_MarketState 속성을 지 원하는 marketState 필드를 volatile로 표시 됩니다

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

BroadcastMarketStateChange 및 BroadcastMarketReset 메서드를 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외는 이미 살펴보았습니다 BroadcastStockPrice 메서드와 비슷합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버를 호출할 수 있는 클라이언트에서 추가 기능

UpdateStockPrice 함수는 이제 표 및 주식 종목 표시를 모두 처리 하 고 jQuery.Color 빨간색 및 녹색 플래시를 사용 하 여 키를 누릅니다.

새 함수 *SignalR.StockTicker.js* 설정 / 해제 단추에 따라 상태를 홍보 하는 주식 종목 창 가로 스크롤이 시작 하거나 중지 합니다. 여러 함수 ticker.client에 추가 되는 합니다 [함수를 확장 하는 jQuery](http://api.jquery.com/jQuery.extend/) 추가 하는 데 사용 됩니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설정

있기 위해 몇 가지 추가 작업 후 클라이언트 연결을 설정 합니다: 시장 열림 또는 닫힘 적절 한 marketOpened 또는 marketClosed 함수를 호출 하 고 단추에 대 한 server 메서드 호출을 연결 하기 위해 인지 확인 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

서버 메서드 반드시 자리까지 단추까지 연결이 설정 되 면 제공 되기 전에 서버 메서드를 호출 하려면 코드를 시도할 수 없습니다 있도록 합니다.

<a id="nextsteps"></a>

## <a name="next-steps"></a>다음 단계

이 자습서에서는 정기적으로와 모든 클라이언트에서 알림 응답에서 연결 된 모든 클라이언트에 게 서버에서 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다. 다중 스레드 singleton 인스턴스를 사용 하 여 서버 상태를 유지 하는 패턴 멀티 플레이어 온라인 게임 시나리오에도 수. 있습니다 예를 들어 참조 [SignalR을 기반으로 하는 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.

피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하세요. [Getting Started with SignalR](introduction-to-signalr.md) 하 고 [SignalR을 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)합니다.

고급 SignalR 개발 개념에 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [ASP.NET SignalR](../../index.md)
- [SignalR 프로젝트](http://signalr.net/)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

Azure SignalR 응용 프로그램을 배포 하는 방법은 연습을 참조 하세요 [Azure App Service에서 Web apps를 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다. Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.
