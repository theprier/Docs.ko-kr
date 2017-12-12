---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: "자습서: ASP.NET SignalR과 서버 브로드캐스트 1.x | Microsoft Docs"
author: pfletcher
description: "이 자습서에는 ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버는 communic 브로드캐스트 수단 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/10/2013
ms.topic: article
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: afb2fa9b3dfd80a2aa49fffae71965fc2098442f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>자습서: ASP.NET SignalR과 서버 브로드캐스트 1.x
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서에는 ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트 클라이언트에 전달 되는 통신 서버에 의해 시작 된 것을 의미 합니다. 이 시나리오는 클라이언트에 전달 되는 통신 하나 이상의 클라이언트에 의해 시작 됩니다 채팅 응용 프로그램과 같은 피어 투 피어 시나리오 보다 다른 프로그래밍 방식이 필요 합니다.
> 
> 이 자습서에서 만들 수 있는 응용 프로그램은 주식 시세를, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이트합니다.
> 
> 이 자습서에 대 한 의견을 기다리겠습니다. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)합니다.


## <a name="overview"></a>개요

[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지는 Visual Studio 프로젝트에 샘플 시뮬레이션 주식 시세 응용 프로그램을 설치 합니다. 이 자습서의 첫 번째 부분에서는 처음부터 해당 응용 프로그램의 단순화 된 버전을 만듭니다. 자습서의 나머지 부분에서는 NuGet 패키지를 설치 하 고 추가 기능 및 생성 된 코드를 검토 합니다.

주식 시세 응용 프로그램 종류 하려는 "밀어넣기" 또는 브로드캐스트, 알림 주기적으로 연결 된 모든 클라이언트에 서버에서 실시간 응용 프로그램의 대표 하는 합니다.

이 자습서의 첫 번째 부분을 만들 것인지를 응용 프로그램에는 주식 데이터로 구성 된 표가 표시 됩니다.

![StockTicker 초기 버전](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

정기적으로 서버 임의로 주가 업데이트 되 고 모든 연결 된 클라이언트에 업데이트를 푸시합니다. 브라우저 숫자 및 기호는 **변경** 및  **%**  열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다. 모두 동일한 데이터 및 표시 된 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 열고 합니다.

이 자습서에는 다음 섹션이 포함 됩니다.

- [필수 조건](#prerequisites)
- [프로젝트 만들기](#createproject)
- [SignalR NuGet 패키지 추가](#nugetpackages)
- [서버 코드를 설정](#server)
- [클라이언트 코드를 설정](#client)
- [응용 프로그램 테스트](#test)
- [로깅을 사용 하도록 설정](#enablelogging)
- [설치 하 고 전체 StockTicker 샘플을 검토 합니다.](#fullsample)
- [다음 단계](#nextsteps)

> [!NOTE]
> 응용 프로그램을 작성 하는 단계를 진행 하도록 않으려면 새 SignalR.Sample 패키지를 설치할 수 있습니다 **빈 ASP.NET 웹 응용 프로그램** 프로젝트를 연 다음이 절차에 대 한 정보는 코드를 읽어야 합니다. 자습서의 첫 번째 부분에서는 SignalR.Sample 코드의 하위 집합에 설명 하 고 두 번째 부분에서는 SignalR.Sample 패키지에 추가 된 기능의 주요 기능에 설명 합니다.


<a id="prerequisites"></a>

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 Visual Studio 2012 또는 2010 s p 1이 컴퓨터에 설치 되어 있는지 확인 합니다. Visual Studio가 없는 경우 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 웹에 대 한는 무료 Visual Studio 2012 Express를 가져오려는 합니다.

Visual Studio 2010를 설정한 경우 확인 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 가 설치 되어 있습니다.

<a id="createproject"></a>

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. **파일** 메뉴 클릭 **새 프로젝트**합니다.
2. 에 **새 프로젝트** 대화 상자에서 **C#** 아래 **템플릿** 선택 **웹**합니다.
3. 선택 된 **ASP.NET 빈 웹 응용 프로그램** 서식 파일을 프로젝트 이름 *SignalR.StockTicker*를 클릭 하 고 **확인**합니다.

    ![새 프로젝트 대화 상자](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>SignalR NuGet 패키지 추가

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>SignalR 및 JQuery NuGet 패키지 추가

프로젝트에 NuGet 패키지를 설치 하 여 SignalR 기능을 추가할 수 있습니다.

1. 클릭 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다.
2. 패키지 관리자에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR 패키지 종속성으로 다양 한 기타 NuGet 패키지를 설치합니다. 설치가 완료 되는 경우 ASP.NET 응용 프로그램에서 SignalR을 사용 하는 데 필요한 서버 및 클라이언트 구성 요소를 모두 수 있습니다.

<a id="server"></a>

## <a name="set-up-the-server-code"></a>서버 코드를 설정

이 섹션에서는 서버에서 실행 하는 코드를 설정 합니다.

### <a name="create-the-stock-class"></a>스톡 클래스 만들기

사용 하 여 저장 하 고는 재고에 대 한 정보를 전송 하는 재고 모델 클래스를 만들어 시작 합니다.

1. 프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *Stock.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    주식을 만들 때 설정 하는 두 속성은 기호 (예를 들어 microsoft MSFT) 및 가격입니다. 다른 속성 가격 설정 하는 방법 및 시기에 따라 달라 집니다. 처음에 가격을 설정할 때 값을 가져옵니다 DayOpen에 전파 됩니다. DayOpen 가격 간의 차이 기반으로 후속 경우가 가격 변경 설정 PercentChange 속성 값을 계산 합니다.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>StockTicker 및 StockTickerHub 클래스 만들기

서버-클라이언트 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다. SignalR 허브 클래스에서 파생 되는 StockTickerHub 클래스는 클라이언트에서 연결 및 메서드 호출을 받고 처리 합니다. 주식 데이터를 유지 관리 하 고 실행을 주기적으로 클라이언트 연결 독립적으로 가격 업데이트를 트리거하는 타이머 개체에 있어야 합니다. 허브 인스턴스를 일시적으로 하기 때문에 허브 클래스에 이러한 함수를 넣을 수 없습니다. 허브 클래스 인스턴스를 연결 및 클라이언트에서 호출을 서버와 같은 허브에 각 작업에 대해 생성 됩니다. 따라서 StockTicker 이름을 지정 하는 별도 클래스에서 실행 하는 주식 데이터를 유지 하 고, 가격을 업데이트, 브로드캐스트하 price 업데이트 메커니즘에서.

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

까다롭기 때문에 각 StockTickerHub 인스턴스로부터 단일 StockTicker 인스턴스에 대 한 참조를 설정 하는 서버에서 실행 되도록 StockTicker 클래스의 인스턴스가 하나씩 하려는 있습니다. StockTicker 클래스에서 StockTicker 허브 클래스가 아닙니다. 하지만 주식 데이터 개이고 업데이트 트리거 때문에 클라이언트에 브로드캐스트할 수 있어야 합니다. 따라서 StockTicker 클래스는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조를 가져올 해야 합니다. 클라이언트에 브로드캐스트하는 SignalR 연결 컨텍스트 개체를 유도할 수 있습니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 항목 추가**합니다.
2. Visual Studio 2012를 설정한 경우는 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=279941), 클릭 **웹** 아래 **Visual C#** 선택 하 고는 **SignalR허브클래스** 항목 템플릿을 합니다. 그렇지 않은 경우 선택 된 **클래스** 템플릿.
3. 클래스의 새 이름을 *StockTickerHub.cs*, 클릭 하 고 **추가**합니다.

    ![StockTickerHub.cs 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [허브](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스는 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 하는 데 사용 합니다. 메서드가 두 개를 정의 하는: `GetAllStocks()`합니다. 클라이언트가 서버에 처음 연결을 주식의 현재 가격으로 모든 목록을 가져오려면이 메서드를 호출 합니다. 메서드는 동기적으로 실행 하 고 반환할 수 `IEnumerable<Stock>` 메모리에서 연결 된 데이터를 반환 하기 때문에 있습니다. 대기 데이터베이스를 조회 하는 웹 서비스 호출 등을 포함 하는 방법을 사용 하면 데이터를 가져올 메서드를 갖는 경우 지정 하는 경우 `Task<IEnumerable<Stock>>` 비동기 처리를 사용할 경우 반환 값으로. 자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드-서버-을 비동기적으로 실행할 때](index.md)합니다.

    HubName 특성 허브 클라이언트에 JavaScript 코드에서 참조 되는 방식을 지정 합니다. 이 특성을 사용 하지 않는 경우 클라이언트의 기본 이름 카멜식 대/소문자를 사용의 버전이 예제의 stockTickerHub 수 있는 클래스 이름입니다.

    StockTicker 클래스를 만들 때 나중에 표시 됩니다, 해당 클래스의 singleton 인스턴스를 정적 인스턴스 속성에 생성 됩니다. 얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 유지 됩니다 StockTicker의 singleton 인스턴스를 해당 인스턴스는 GetAllStocks 메서드 현재 주식 정보를 반환 하는 데 사용 하는 하 합니다.
5. 프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *StockTicker.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    여러 스레드에서 StockTicker 코드의 같은 인스턴스를 실행 하므로 StockTicker 클래스는 threadsafe를 해야 합니다.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>정적 필드에 단일 인스턴스를 저장합니다.

    코드를 정적 초기화 \_인스턴스 필드는 클래스와이 인스턴스가 있는 인스턴스 속성을 지 원하는 유일한 인스턴스인 만들 수 있는 클래스의 생성자를 private으로 표시 되어 있습니다. [초기화 지연](https://msdn.microsoft.com/en-us/library/dd997286.aspx) 에 사용 되는 \_인스턴스 필드를 인스턴스 생성 threadsafe 인지를 확인 하지만 성능 향상을 위해 되지 않습니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    클라이언트가 서버에 연결 될 때마다 별도의 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스 StockTicker singleton 인스턴스를 가져옵니다 StockTicker.Instance 정적 속성에서 StockTickerHub 클래스 앞에서 보았듯이 합니다.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary 주식 데이터를 저장

    생성자가 초기화 하는 \_일부 샘플 주식 데이터 및 GetAllStocks를 사용 하 여 주식 컬렉션 주식을 반환 합니다. 앞서 살펴본 것 처럼 주가이 컬렉션에 클라이언트가 호출할 수 있는 허브 클래스에 서버 메서드로 StockTickerHub.GetAllStocks에 의해 반환 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    주식 컬렉션으로 정의 됩니다는 [ConcurrentDictionary](https://msdn.microsoft.com/en-us/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 유형입니다. 사용할 수 있습니다는 [사전](https://msdn.microsoft.com/en-us/library/xfhwa508.aspx) 개체를 명시적으로 변경 하는 경우 사전을 잠급니다.

    이 샘플 응용 프로그램에 대 한 좋다고 확인 메모리에 응용 프로그램 데이터를 저장 하 고 StockTicker 인스턴스가 삭제 될 때 데이터가 손실 합니다. 실제 응용 프로그램에서 데이터베이스와 같은 백 엔드 데이터 저장소와 함께 작동할 것 있습니다.

    ### <a name="periodically-updating-stock-prices"></a>주가 주기적으로 업데이트

    생성자는 주기적으로 임의의 무휴로 주가 업데이트 하는 메서드를 호출 하는 타이머 개체를 시작 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices는 state 매개 변수에서 null을 전달 하 고 타이머를 통해 호출 됩니다. 사용 된 잠금이 가격을 업데이트 하기 전에 \_updateStockPricesLock 개체입니다. 코드는 다른 스레드를 가격을 업데이트 하 고 목록에서 각 주식의 TryUpdateStockPrice 호출 다음 확인 합니다. TryUpdateStockPrice 메서드 주가 변경할지 여부를 결정 및 양을 변경할 수 있습니다. 주식 가격이 변경 된 경우 연결 된 모든 클라이언트에 브로드캐스트 주가 변경 BroadcastStockPrice 호출 됩니다.

    \_updatingStockPrices 플래그로 표시 되어 [휘발성](https://msdn.microsoft.com/en-us/library/x13ttww7.aspx) 에 대 한 액세스 threadsafe 인지 확인 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    실제 응용 프로그램에서 TryUpdateStockPrice 메서드; 가격을 조회 하는 웹 서비스 호출 것 이 코드에서 임의로 변경 하는 난수 생성기를 사용 합니다.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기

    가격 변경을 여기 StockTicker 개체 들어오므로 모든 연결 된 클라이언트에서 updateStockPrice 메서드를 호출 해야 하는 개체입니다. 허브 클래스 클라이언트 메서드 호출을 위한 API가 있지만 StockTicker 허브 클래스에서 파생 되지 않은 않으며 허브 개체에 대 한 참조를 갖지 않습니다. 따라서 연결 된 클라이언트에 브로드캐스트용 하려면 SignalR 컨텍스트 인스턴스 StockTickerHub 클래스에 대 한 가져오고 하는 클라이언트에서 메서드를 호출할 StockTicker 클래스에 있습니다.

    코드 SignalR 컨텍스트에 대 한 참조의 패스를 참조 하는 생성자를 단일 항목 클래스 인스턴스를 만들 때 가져오고 생성자 클라이언트 속성에 배치 합니다.

    다음 두 가지 컨텍스트를 한 번만 이유: 컨텍스트를 얻는 것은 비용이 많이 드는 작업 및 클라이언트에 전송 된 메시지의 의도 한 순서는 유지 하는 사용 하면 한 번 하 게 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    컨텍스트의 클라이언트 속성을 가져오고 StockTickerClient 속성에 넣으면 허브 클래스에서와 같이 동일한 검색 하는 메서드를 호출할 클라이언트 코드를 작성할 수 있습니다. 예를 들어, 모든 클라이언트에 브로드캐스트하 Clients.All.updateStockPrice(stock)를 작성할 수 있습니다.

    아직; BroadcastStockPrice를 호출 하는 updateStockPrice 메서드 없음 클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다. Clients.All 런타임에 식을 평가할 수는 동적 이므로 updateStockPrice 여기를 참조할 수 있습니다. 이 메서드 호출이 실행 되 면 SignalR에서 메서드 이름과 매개 변수 값에 클라이언트에 보내고 클라이언트에 updateStockPrice 라는 메서드를 해당 메서드는 호출 되 고 매개 변수 값에 전달 됩니다.

    Clients.All 모든 클라이언트에 보내는 것을 의미 합니다. SignalR은 클라이언트 또는에 보내도록 클라이언트 그룹을 지정할 다른 옵션을 제공 합니다. 자세한 내용은 참조 [HubConnectionContext](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버를 가로채 고 SignalR에 액세스 하는 URL을 알고 있어야 합니다. 일부 코드를 추가한 작업을 수행 하는 *Global.asax* 파일입니다.

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새 항목 추가**합니다.
2. 선택 된 **전역 응용 프로그램 클래스** 템플릿을 항목 선택한 다음 클릭 **추가**합니다.

    ![Global.asax 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. SignalR 경로 등록 코드를 응용 프로그램 추가\_Start 메서드:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    기본적으로 모든 SignalR 트래픽에 대 한 기본 URL은 "/ signalr", "/ signalr/허브" 응용 프로그램에 있는 모든 허브에 대 한 프록시를 정의 하는 동적으로 생성 된 JavaScript 파일을 검색 하는 데 사용 됩니다. MapHubs 메서드에 포함 인스턴스의 서로 다른 기본 URL과 특정 SignalR 옵션을 지정할 수 있는 오버 로드는 [HubConfiguration](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) 클래스입니다.
4. 사용 하 여 추가 파일 맨 위에 있는 문.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. 저장 하 고 닫습니다는 *Global.asax* 파일과 프로젝트를 빌드합니다.

이제 서버 코드를 설정을 완료 했습니다. 다음 섹션에서 클라이언트를 설정 합니다.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>클라이언트 코드를 설정

1. 프로젝트 폴더에 새 HTML 파일을 만들고 이름을 *StockTicker.html*합니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML 5 개의 열, 머리글 행 및 모든 5 개의 열에 걸쳐 있는 하나의 셀에 데이터 행이 있는 테이블을 만듭니다. 데이터 행 "로드 중..."를 표시 하 고 일시적으로 응용 프로그램을 시작 하는 경우에 표시 됩니다. JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여의 전체 행에 추가할 합니다.

    스크립트 태그는 jQuery 스크립트 파일, SignalR core 스크립트 파일, SignalR 프록시 스크립트 파일 및 나중에 만드는 StockTicker 스크립트 파일을 지정 합니다. "/ Signalr/허브" URL을 지정 하는 SignalR 프록시 스크립트 파일을 동적으로 생성 및 StockTickerHub.GetAllStocks에 대 한이 예에서 허브 클래스에 메서드에 대 한 프록시 메서드를 정의 합니다. 원하는 경우 생성할 수 있습니다이 JavaScript 파일을 수동으로 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) MapHubs 메서드 호출에서 동적 파일 만들기를 사용 하지 않도록 설정 합니다.
3. > [!IMPORTANT]
 > JavaScript 파일에 참조 하는지 확인 *StockTicker.html* 올바른지 합니다. 즉, 인지 확인 하거나 스크립트 태그 (예제에서 1.8.2)에서 jQuery 버전을 프로젝트의 jQuery 버전과 같은 *스크립트* 폴더 인지 확인 하거나 스크립트 태그의 SignalR 버전 SignalR과 동일 하 고 프로젝트의 버전 *스크립트* 폴더입니다. 필요에 따라 스크립트 태그의 파일 이름을 변경 합니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*, 클릭 하 고 **시작 페이지로 설정**합니다.
5. 프로젝트 폴더에 새 JavaScript 파일을 만들고 이름을 *StockTicker.js*...
6. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $.connection SignalR 프록시를 참조합니다. 코드는 StockTickerHub 클래스에 대 한 프록시에 대 한 참조를 가져오고 주식 종목 변수에 저장 합니다. 프록시 이름은 [HubName] 특성으로 설정 된 이름:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    모든 변수 및 함수를 정의한 후 파일에 코드의 마지막 줄 SignalR 시작 함수를 호출 하 여 SignalR 연결을 초기화 합니다. 비동기적으로 실행 하 고 반환 하는 시작 함수는 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/), 비동기 작업이 완료 될 때 호출할 함수를 지정 완료 함수를 호출할 수 있습니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init 함수는 서버에서 getAllStocks 함수를 호출 하 고 주식 테이블을 업데이트 하려면 서버를 반환 하는 정보를 사용 하 여 합니다. 것을 확인할 기본적으로 카멜식 대/소문자 클라이언트 메서드 이름은 파스칼식 대 서버에 있지만 사용 하도록 합니다. 카멜식 대 / 소문자 규칙은 개체가 아니라 방법에만 적용 됩니다. 예를 들어 재고를 참조할 수도 있습니다. 기호 및 stock 합니다. 가격, stock.symbol 말거나 stock.price 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    완전히 다른 메서드 이름을 사용 하려는 경우 수 데코레이팅되 HubMethodName 특성을 사용 하는 허브 메서드를 같은 방식으로 또는 클라이언트에서 파스칼식 대/소문자를 사용 하려는 경우 허브 클래스 자체 HubName 특성으로 데코레이팅된 합니다.

    Init 메서드에 테이블 행에 대 한 HTML 스톡 개체의 서식 속성을 호출 formatStock 하 여 서버에서 받은 각 스톡 개체에 대해 만들어지고 다음 호출 하며 (맨 위에 있는 정의 된 *StockTicker.js*) 자리 표시자를 대체할 rowTemplate 변수에 스톡 개체 속성 값을 사용 합니다. 결과 HTML 스톡 테이블에 다음 추가 됩니다.

    비동기 시작 함수가 완료 된 후에 실행 되는 콜백 함수로 전달 하 여 초기화를 호출 합니다. 시작을 호출한 후 별도 JavaScript 문으로 초기화를 호출 하는 경우 함수를 오류가 발생 시작 함수는 연결 구성 완료를 기다리지 않고 즉시 실행 됩니다. 이 경우 init 함수 서버 연결을 설정 하기 전에 getAllStocks 함수를 호출 하려고 합니다.

    서버는 주식 가격 변경 되 면 연결 된 클라이언트에는 updateStockPrice를 호출 합니다. 함수는 사용할 수 있도록 호출 하는 서버에서 stockTicker 프록시의 클라이언트 속성에 추가 됩니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice 함수 init 함수에서와 같이 동일한 방식으로 테이블 행에는 서버에서 받은 스톡 개체의 형식을 지정 합니다. 그러나 테이블에 행을 추가 하는 대신 재고의 현재 행 테이블에서 찾아 해당 행을 새 항목으로 대체 합니다.

<a id="test"></a>

## <a name="test-the-application"></a>응용 프로그램 테스트

1. F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.

    스톡 테이블의 "로드 중..." 줄을 다음 초기 주식 데이터를 표시 하는 짧은 지연 후 처음에 표시 하 고 변경 하려면 주식 가격을 시작 하는 합니다.

    ![로드](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![초기 스톡 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![서버에서 변경 내용을 수신할 주식 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. 브라우저 주소 표시줄에서 URL을 복사 하 고 하나 이상의 새 브라우저 창에 붙여 넣습니다.

    초기 스톡 표시 된 첫 번째 브라우저와 같으면 이며 변경이 동시에 발생 합니다.
3. 모든 브라우저를 닫고 하 고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.

    StockTicker singleton 개체는 서버에서 실행 스톡 테이블 디스플레이 주식 변경 하려면 계속 해 서 표시 되므로 계속 합니다. (숫자 값 변경에 0이 초기 표를 참조 하지 않습니다.)
4. 브라우저를 닫습니다.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>로깅 사용

SignalR은 클라이언트에서 문제 해결에 도움이 되도록 설정할 수 있는 기본 제공 로깅 기능을 있습니다. 이 섹션의 로깅을 사용 하도록 설정 및 어떻게 로그 알려 SignalR를 사용 하는 다음 전송 방법을 보여 주는 예제를 참조 하십시오.

- [Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8와 현재 브라우저에서 지원 합니다.
- [서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)Internet Explorer 이외의 브라우저에서 지원 합니다.
- [Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)Internet Explorer에서 지원 합니다.
- [Ajax 긴 폴링과](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.

지정된 된 연결에 대 한 SignalR을 지 원하는 서버와 클라이언트 모두 최상의 전송 방법을 선택 합니다.

1. 열기 *StockTicker.js* 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. F5 키를 눌러 프로젝트를 실행합니다.
3. 브라우저의 개발자 도구 창을 열고 로그를 참조 하 고 콘솔을 선택 합니다. Signalr에 대 한 새 연결 전송 방법을 협상의 로그를 보려면 페이지를 새로 고쳐야 할 수 있습니다.

    Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 Websocket입니다.

    ![IE 10 IIS 8 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 iframe 합니다.

    ![IE 10 콘솔, IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    Firefox에서 Firebug 추가 기능 설치 콘솔 창에 얻으려고 합니다. Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 Websocket입니다.

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Windows 7 (IIS 7.5) Firefox 19를 실행 하는 경우 전송 방법은 서버에서 전송 하는 이벤트입니다.

    ![Firefox 19 IIS 7.5 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>설치 하 고 전체 StockTicker 샘플을 검토 합니다.

StockTicker 응용 프로그램으로 설치 되는 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지를 처음부터 방금 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다. 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 해당 구현 하는 코드를 검토 합니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR.Sample NuGet 패키지 설치

1. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.
2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **온라인**, 입력 *SignalR.Sample* 에 **온라인 검색** 상자를 선택한 다음 클릭 **설치** 에 **SignalR.Sample** 패키지 합니다.

    ![SignalR.Sample 패키지 설치](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. 에 *Global.asax* 파일는 RouteTable.Routes.MapHubs() 주석; 응용 프로그램의 앞부분에 나오는 추가한 줄\_메서드를 시작 합니다.

    코드 *Global.asax* SignalR.Sample 패키지에서 SignalR 경로 등록 하기 때문에 더 이상 필요 없는 *앱\_Start/RegisterHubs.cs* 파일:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    어셈블리 특성에 의해 참조 되는 WebActivator 클래스 SignalR.Sample 패키지의 종속성으로 설치 됩니다 WebActivatorEx NuGet 패키지에 포함 됩니다.
4. **솔루션 탐색기**를 확장 하 고는 *SignalR.Sample* SignalR.Sample 패키지를 설치 하 여 생성 된 폴더입니다.
5. 에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*, 클릭 하 고 **시작 페이지로 설정**합니다.

    > [!NOTE]
    > SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다는 버전의 jQuery에서 사용 하 여 *스크립트* 폴더입니다. 새 *StockTicker.html* 패키지에 설치 하는 파일의 *SignalR.Sample* 폴더가 원래의실행하려면패키지를설치하는jQuery버전와동기화됩니다.*StockTicker.html* 파일을 다시, jQuery 참조는 스크립트 태그를 먼저 업데이트 해야 할 수 있습니다.

### <a name="run-the-application"></a>응용 프로그램 실행

1. F5 키를 눌러 응용 프로그램을 실행합니다.

    표에서 했 듯이 외에도 전체 주식 시세 응용 프로그램에 동일한 주식 데이터를 표시 하는 가로 스크롤 막대가 창을 보여 줍니다. 처음으로 응용 프로그램을 실행 하면 "시장"는 "닫힘" 있는데 정적 그리드 및 없는 스크롤 하는 주식 종목 창을 표시 합니다.

    ![StockTicker 화면 시작](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    클릭할 때 **시장**, **주식 시세 라이브** 가로로 스크롤할 수 상자 시작 하 고 서버에 임의의 으로만 주가 변경 사항을 브로드캐스트하는 주기적으로 시작 합니다. 주식 시세에서 사용자가 둘 다 변경는 **재고 테이블 라이브** 그리드 및 **주식 시세 라이브** 상자 업데이트 됩니다. 특정 주식 가격 변경을 양수 이면 재고는 면 녹색 배경을 표시 및 변경이 음수 이면 재고가 하면 빨간색 배경을 표시 됩니다.

    ![StockTicker 앱 시장 열](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    **닫기 시장** 단추는 변경 내용을 중지 하 고 주식 종목 스크롤 중지 및 **재설정** 가격 시작 되기 전에 단추를 초기 상태로 모든 주식 데이터를 초기화 합니다. 브라우저 창을 열고 동일한 URL로 이동 하는 경우 각 브라우저에서 같은 시간에 동적으로 업데이트 하는 같은 데이터 표시 됩니다. 단추 중 하나를 클릭 하면 모든 브라우저 동시에 같은 방법으로 응답 합니다.

### <a name="live-stock-ticker-display"></a>라이브 주식 종목 표시

**주식 시세 라이브** 은 CSS 스타일에 의해 단일 줄으로 포맷 된 div 요소에는 순서가 지정 되지 않은 목록을 표시 합니다. 주식 종목 초기화 되 고 동일한 방식으로 테이블을 업데이트:의 자리 표시자를 대체 하 여는 &lt;li&gt; 템플릿 문자열을 동적으로 추가 하는 &lt;li&gt; 요소를 사용 하 여 &lt;ul&gt; 요소입니다. div. 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백을 변경 하려면 jQuery 애니메이션 효과 주기 함수를 사용 하 여 수행 됩니다 스크롤

주식 시세 HTML:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

주식 시세 CSS:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

JQuery 코드를 사용 하면를 스크롤합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트를 호출할 수 있는 서버에서 추가 메서드

StockTickerHub 클래스 클라이언트가 호출할 수 있는 4 개의 추가 메서드를 정의 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

OpenMarket, CloseMarket, 및 재설정 페이지 맨 위에 있는 단추에 대 한 응답으로 호출 됩니다. 모든 클라이언트에 즉시 전파 되는 상태 변경 트리거 한 클라이언트의 패턴을 보여 줍니다. 이러한 각 방법의에서 메서드를 호출 StockTicker 클래스 인해 영향을 주는 시장 상태 변경 및 새 상태를 다음 브로드캐스트합니다.

StockTicker 클래스에서 시장 상태 MarketState 열거형 값을 반환 하는 MarketState 속성에 의해 유지 관리 됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

각 시장 상태를 변경 하는 방법의 잠금 블록 안에 StockTicker 클래스는 threadsafe 해야 하기 때문에 다음과 같이

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

이 코드를 threadsafe 되는지는 \_MarketState 속성을 지 원하는 marketState 필드를 volatile로 표시 됩니다

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

BroadcastMarketStateChange 및 BroadcastMarketReset 메서드는 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외 BroadcastStockPrice 메서드가 이미 본 것과 비슷합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버를 호출할 수 있는 클라이언트에서 추가 기능

JQuery.Color를 사용 하 여 색을 빨간색 및 녹색 플래시 및 updateStockPrice 함수는 이제 주식 종목 표시와 눈금을 모두 처리 합니다.

새 기능은 *SignalR.StockTicker.js* 설정 / 해제 단추에 따라 상태를 홍보 하는 주식 종목 창 가로 스크롤을 시작 하거나 중지 합니다. 여러 함수가 ticker.client에 추가 되 고 되는 [jQuery 확장 함수](http://api.jquery.com/jQuery.extend/) 에 추가 하는 데 사용 됩니다.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설치

몇 가지 추가 작업을 수행 해야 클라이언트는 연결 되 면, 있기: 시장을 열려 있거나 적절 한 marketOpened 또는 marketClosed 함수를 호출 하 고 단추에 대 한 서버 메서드 호출 연결 하기 위해 닫혀 있는지 확인 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

서버 메서드 반드시 자리까지 나타날 때까지 단추는 연결이 설정 된 후 코드 없습니다 제공 되기 전에 서버 메서드를 호출 하려고 하 합니다.

<a id="nextsteps"></a>

## <a name="next-steps"></a>다음 단계

이 자습서에서는 모든 클라이언트에서 알림에 대 한 응답에서 및 주기적으로 연결 된 모든 클라이언트에 서버에서 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 배웠습니다. 다중 스레드 singleton 인스턴스를 사용 하 여 서버 상태를 유지 하는 패턴 사용할 수도 있습니다도 멀티 플레이 온라인 게임 시나리오에서 합니다. 예를 들어 참조 [SignalR을 기반으로 하는 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.

피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하십시오. [SignalR 시작](index.md) 및 [SignalR로 실시간 업데이트](index.md)합니다.

SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR 프로젝트](http://signalr.net/)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
