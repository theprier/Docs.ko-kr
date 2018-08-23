---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR에서 종속성 주입 1.x | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: d59ca85f1005b08ff52ded61d94323dabdb40d0a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839118"
---
<a name="dependency-injection-in-signalr-1x"></a>SignalR에서 종속성 주입 1.x
====================
하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

종속성 주입은 쉽게 (모의 개체를 사용 하 여) 테스트에 대 한 중 하나는 개체의 종속성, 대체 또는 런타임 동작을 변경 하려면 개체 간에 하드 코드 된 종속성을 제거 하는 방법입니다. 이 자습서에는 signalr에서 종속성 주입을 수행 하는 방법을 보여 줍니다. 또한 SignalR을 사용 하 여 IoC 컨테이너를 사용 하는 방법을 보여 줍니다. IoC 컨테이너는 종속성 주입을 위한 범용 프레임 워크입니다.

## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

종속성 주입을 사용 하 여 이미 익숙한 경우이 섹션을 건너뜁니다.

*종속성 주입* (DI)은 개체 자체 종속성 생성을 담당 하지는 패턴입니다. DI를 유도 하 여 간단한 예는 다음과 같습니다. 메시지를 기록 하는 개체를 있다고 가정 합니다. 로깅 인터페이스를 정의할 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

개체를 만들 수 있습니다는 `ILogger` 메시지를 기록 합니다.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

가장 적합 한 디자인 것만이 방법이 작동 합니다. 대체 하려는 경우 `FileLogger` 상호 `ILogger` 수정 해야 구현 `SomeComponent`합니다. 다른 많은 개체가 사용 하는 예 `FileLogger`, 이들 모두를 변경 해야 합니다. 확인 하려는 경우 또는 `FileLogger` 단일 해야 응용 프로그램 전체에서 변경 해야 합니다.

"삽입" 하는 것이 좋습니다는 `ILogger` 개체로-예를 들어, 생성자 인수를 사용 하 여:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

개체는 선택 하 여 처리 하지 않습니다 이제 `ILogger` 사용 하도록 합니다. Swich 있습니다 `ILogger` 에 종속 된 개체를 변경 하지 않고 구현 합니다.

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

이 패턴 이라고 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다. 또 다른 패턴은 setter 메서드 또는 속성을 통해 종속성을 설정한 setter 주입 합니다.

## <a name="simple-dependency-injection-in-signalr"></a>SignalR에서 간단한 종속성 주입

이 자습서에서 채팅 응용 프로그램을 고려해 야 [SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)합니다. 해당 응용 프로그램에서 허브 클래스는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

채팅 메시지를 보내기 전에 서버에 저장 하려는 경우 이 기능을 추상화 하는 인터페이스를 정의 하 고 DI를 사용 하 여 인터페이스에 삽입할 수 있습니다는 `ChatHub` 클래스입니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

문제는이 SignalR 응용 프로그램을 직접 만들지 않습니다 hubs; SignalR에서이 만듭니다. 기본적으로 SignalR 허브 클래스에 매개 변수가 없는 생성자가 필요 합니다. 그러나 쉽게 허브 인스턴스를 만드는 함수를 등록 하 고 수 DI를 수행 하려면이 함수를 사용 합니다. 함수를 호출 하 여 등록 **GlobalHost.DependencyResolver.Register**합니다.

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

사이트를 만드는 데 필요한 때마다 SignalR는이 익명 함수를 호출 하는 이제는 `ChatHub` 인스턴스.

## <a name="ioc-containers"></a>IoC 컨테이너

위의 코드는 간단한 사례에 적합 합니다. 하지만이 작성 해야 합니다.

[!code-css[Main](dependency-injection/samples/sample8.css)]

많은 종속성이 있는 복잡 한 응용 프로그램에서는이 "연결" 코드를 많이 작성 해야 합니다. 이 코드는 종속성 중첩 된 경우에 특히을 유지 하기 어려울 수 있습니다. 또한 단위 테스트 하는 것이 어렵습니다.

하나의 솔루션 IoC 컨테이너를 사용 하는 것입니다. IoC 컨테이너는 종속성을 관리 하는 일을 담당 하는 소프트웨어 구성 요소입니다. 컨테이너로 형식을 등록 하 고이 정보를 개체를 만드는 컨테이너를 사용 합니다. 컨테이너는 자동으로 종속성 관계를 파악합니다. 많은 IoC 컨테이너를 사용 하면 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"는 "제어 반전"에 대 한 일반적인 패턴을 설정 하는 프레임 워크 응용 프로그램 코드를 호출 하는 경우이 합니다. IoC 컨테이너 생성 개체를 "반전" 컨트롤의 일반적인 흐름입니다.


## <a name="using-ioc-containers-in-signalr"></a>SignalR의 IoC 컨테이너 사용

채팅 응용 프로그램 IoC 컨테이너에서 에게도 너무 간단 때문일 수 있습니다. 대신 살펴보겠습니다 합니다 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플입니다.

StockTicker 샘플 두 가지 주요 클래스를 정의합니다.

- `StockTickerHub`클라이언트 연결을 관리 하는: 허브 클래스입니다.
- `StockTicker`: 단일은 주식 시세를 보유 하 고 정기적으로 업데이트 합니다.

`StockTickerHub` 에 대 한 참조를 보유 합니다 `StockTicker` singleton을 하는 동안 `StockTicker` 에 대 한 참조를 보유 합니다 **IHubConnectionContext** 에 대 한를 `StockTickerHub`. 이 인터페이스를 사용 하 여 통신할 `StockTickerHub` 인스턴스. (자세한 내용은 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md).)

이러한 종속성을 약간 분리 IoC 컨테이너를 사용할 수 있습니다. 먼저 간소화 합니다 `StockTickerHub` 및 `StockTicker` 클래스입니다. 다음 코드에서 필자 했습니다 주석 부분에서는 필요 하지 않습니다.

매개 변수가 없는 생성자를 제거 `StockTicker`합니다. 대신 항상 DI 허브를 만들려면 사용 합니다.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

StockTicker, singleton 인스턴스를 제거 합니다. 나중에, StockTicker 수명을 제어 하려면 IoC 컨테이너를 사용 하겠습니다. 또한 생성자는 공용 확인 합니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다 다음으로, `StockTicker`합니다. 이 인터페이스 사용 하 여 분리 된 `StockTickerHub` 에서 `StockTicker` 클래스입니다.

Visual Studio를 사용 하면이 종류의 리팩터링 쉽게 합니다. StockTicker.cs 파일을 열고 마우스 오른쪽 단추로 클릭 합니다 `StockTicker` 선택한 클래스 선언인 **리팩터링** ... **인터페이스 추출**합니다.

![](dependency-injection/_static/image1.png)

에 **인터페이스 추출** 대화 상자에서 클릭 **모두 선택**합니다. 다른 기본값을 그대로 둡니다. **확인**을 클릭합니다.

![](dependency-injection/_static/image2.png)

Visual Studio 이라는 새 인터페이스를 만들고 `IStockTicker`, 변경 및 `StockTicker` 에서 파생 `IStockTicker`합니다.

IStockTicker.cs 파일을 열고 인터페이스를 변경 **공용**합니다.

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

에 `StockTickerHub` 클래스의 두 인스턴스를 변경 합니다 `StockTicker` 에 `IStockTicker`:

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

만들기는 `IStockTicker` 인터페이스 반드시 필요 하지 않지만 응용 프로그램의 구성 요소 간의 결합을 줄이는 데 DI 유용한 방법을 보여 주려고 합니다.

## <a name="add-the-ninject-library"></a>Ninject 라이브러리 추가

.NET에 대 한 많은 공개 소스 IoC 컨테이너가 있습니다. 이 자습서에서는 사용 하 여 [Ninject](http://www.ninject.org/)합니다. (다른 인기 있는 라이브러리 포함 [Castle Windsor](http://www.castleproject.org/)를 [Spring.Net](http://www.springframework.net/)를 [Autofac](https://code.google.com/p/autofac/)를 [Unity](https://github.com/unitycontainer/unity), 및 [StructureMap ](http://docs.structuremap.net).)

NuGet 패키지 관리자 설치를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)합니다. Visual Studio에서에서 합니다 **도구가** 메뉴 선택 **라이브러리 패키지 관리자** | **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>SignalR 종속성 확인자를 대체 합니다.

SignalR 내 Ninject를 사용 하려면에서 파생 된 클래스를 만듭니다 **DefaultDependencyResolver**합니다.

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

이 클래스는 재정의 **GetService** 하 고 **GetServices** 메서드 **DefaultDependencyResolver**합니다. SignalR 허브 인스턴스 뿐만 아니라 SignalR에서 내부적으로 사용 하는 다양 한 서비스를 포함 하 여 런타임 시 다양 한 개체를 만들려면 이러한 메서드를 호출 합니다.

- 합니다 **GetService** 메서드 형식의 단일 인스턴스를 만듭니다. Ninject 커널의 호출 하려면이 메서드를 재정의 **TryGet** 메서드. 해당 메서드가 null을 반환 하는 경우 기본 확인자를 대체 합니다.
- 합니다 **GetServices** 메서드는 지정 된 형식의 개체의 컬렉션을 만듭니다. 기본 해결 프로그램에서 결과 사용 하 여 Ninject에서 결과 연결 하려면이 메서드를 재정의 합니다.

## <a name="configure-ninject-bindings"></a>Ninject 바인딩 구성

이제 형식 바인딩을 선언 하 Ninject 사용 하겠습니다.

RegisterHubs.cs 파일을 엽니다. 에 `RegisterHubs.Start` 메서드를 Ninject 호출 Ninject 컨테이너를 만들어야 합니다 *커널*.

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

이 사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

에 대 한 바인딩을 만들 `IStockTicker` 다음과 같습니다.

[!code-html[Main](dependency-injection/samples/sample17.html)]

이 코드는 두 가지 라는 됩니다. 응용 프로그램에서 필요할 때마다 첫 번째는 `IStockTicker`, 커널의 인스턴스를 만들도록 `StockTicker`합니다. 두 번째는 `StockTicker` 클래스는 단일 개체로 생성 해야 합니다. Ninject 개체의 인스턴스를 하나 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.

에 대 한 바인딩을 만들 **IHubConnectionContext** 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

이 코드 creatres 반환 하는 익명 함수는 **IHubConnection**합니다. 합니다 **WhenInjectedInto** 메서드를 만들 때만이 함수를 사용 하려면 Ninject 지시 `IStockTicker` 인스턴스. 이유는 SignalR 만들어지는 **IHubConnectionContext** 내부적으로 인스턴스 SignalR을 만드는 방법을 재정의를 만들 필요가 없습니다. 이 함수에만 적용 됩니다는 `StockTicker` 클래스입니다.

종속성 확인자에 전달 된 **MapHubs** 메서드:

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

SignalR은에 지정 된 해결 프로그램을 사용 하는 이제 **MapHubs**, 기본 해결 프로그램 대신 합니다.

전체 코드 목록은 다음과 같습니다 `RegisterHubs.Start`합니다.

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 f5 키를 누릅니다. 브라우저 창에서 이동 `http://localhost:*port*/SignalR.Sample/StockTicker.html`합니다.

![](dependency-injection/_static/image3.png)

응용 프로그램에 정확히 동일한 기능을 전 합니다. (에 대 한 참조 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md).) 아직 변경 되었습니다. 테스트, 유지 및 발전을 쉽게 코드를 만들었습니다.
