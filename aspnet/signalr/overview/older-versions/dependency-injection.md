---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR의 종속성 주입 1.x | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/15/2013
ms.topic: article
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 6fd155adc9a0aa71b66db7a51062a51fb0c1feca
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26505492"
---
<a name="dependency-injection-in-signalr-1x"></a>SignalR의 종속성 주입 1.x
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

종속성 삽입은 쉽게 (모의 개체를 사용 하 여) 테스트 하기 위해 개체의 종속성, 교체 하거나 런타임 동작을 변경 하려면 개체 간에 하드 코드 된 종속성을 제거 하는 방법입니다. 이 자습서에는 종속성 주입 SignalR 허브에서 수행 하는 방법을 보여 줍니다. 또한 IoC 컨테이너를 사용 하 여 SignalR을 사용 하는 방법을 보여 줍니다. IoC 컨테이너는 종속성 주입을 위한 일반 프레임 워크입니다.

## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

종속성 주입을 사용 하 던 하는 경우이 섹션을 건너뜁니다.

*종속성 주입* DI ()는 개체가 직접 종속성을 만드는 책임이있지 않습니다 패턴입니다. DI를 유도 하기 위해 간단한 예는 다음과 같습니다. 메시지를 기록 하는 개체를 있다고 가정 합니다. 로깅 인터페이스를 정의할 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

개체를 만들 수 있습니다는 `ILogger` 메시지를 기록 하려면:

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

이 방법이 작동 하지만 최상의 디자인 않습니다. 바꾸려는 경우 `FileLogger` 다른 `ILogger` 구현을 수정 해야 할 됩니다 `SomeComponent`합니다. 다른 많은 개체가 사용 supposing `FileLogger`, 모두를 변경 해야 합니다. 확인 하려는 경우 또는 `FileLogger` 를 단일도 해야 응용 프로그램에 걸쳐 변경 해야 합니다.

"삽입" 하는 것이 좋습니다는 `ILogger` 개체로-예를 들어, 생성자 인수를 사용 하 여:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

개체는 선택 하 여 처리 하지 않습니다 이제 `ILogger` 사용 하도록 합니다. Swich 수 `ILogger` 에 종속 된 개체를 변경 하지 않고 구현 합니다.

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

이 패턴 라고 [생성자 삽입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다. 또 다른 패턴은 setter 메서드 또는 속성을 통해 종속성을 설정한 setter 삽입 합니다.

## <a name="simple-dependency-injection-in-signalr"></a>SignalR의 간단한 종속성 주입

이 자습서에서 채팅 응용 프로그램을 생각해 [SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)합니다. 다음은 해당 응용 프로그램에서 허브 클래스가입니다.

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

채팅 메시지를 보내기 전에 서버에 저장 한다고 가정 합니다. 에 대 한 인터페이스를 삽입할 수 DI를 사용 하이 기능을 추상화 하는 인터페이스를 정의할 수 있습니다는 `ChatHub` 클래스입니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

유일한 문제를 SignalR 응용 프로그램을 직접 만들지 않습니다; 허브는 SignalR가 만들어 합니다. 기본적으로 SignalR 허브 클래스에 매개 변수가 없는 생성자가 필요 합니다. 그러나 쉽게 허브 인스턴스를 만드는 함수를 등록 하 고 수 DI를 수행 하려면이 함수를 사용 합니다. 함수를 호출 하 여 등록 **GlobalHost.DependencyResolver.Register**합니다.

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

사이트를 만드는 데 필요한 때마다 SignalR는이 익명 함수를 호출 하는 이제는 `ChatHub` 인스턴스.

## <a name="ioc-containers"></a>IoC 컨테이너

앞의 코드는 간단한 사례에 대 한 문제가 없습니다. 하지만 아직이 작성 해야 했습니다.

[!code-css[Main](dependency-injection/samples/sample8.css)]

많은 종속성이 있는 복잡 한 응용 프로그램에서 많은이 "배선" 코드를 작성 해야 합니다. 특히 종속성 중첩 된 경우이 코드를 유지 하기 어려울 수 있습니다. 단위 테스트에도 어렵습니다.

한 가지 해결 IoC 컨테이너를 사용 하는 것입니다. IoC 컨테이너는 종속성을 관리 하는 소프트웨어 구성 요소입니다. 컨테이너 형식을 등록 하 고이 정보를 개체를 만들 컨테이너를 사용 합니다. 컨테이너는 종속성 관계를 자동으로 알아 합니다. 많은 IoC 컨테이너 개체 수명, 범위 등의 작업을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"은 "컨트롤의 inversion" 되는 일반적인 패턴을 설정 하는 응용 프로그램 코드에는 프레임 워크를 호출 하는 경우이 합니다. IoC 컨테이너 개체에 대 한 구문, 일반적인 제어 흐름을 "반전"입니다.


## <a name="using-ioc-containers-in-signalr"></a>SignalR의 IoC 컨테이너 사용

채팅 응용 프로그램 IoC 컨테이너에서 사용 하기 위해 너무 간단 때문일 수 있습니다. 대신, 살펴보겠습니다는 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플.

StockTicker 샘플 두 가지 주요 클래스를 정의합니다.

- `StockTickerHub`클라이언트 연결을 관리 하는: 허브 클래스입니다.
- `StockTicker`:는 singleton입니다 주가 보유 하 고 정기적으로 업데이트 합니다.

`StockTickerHub`에 대 한 참조를 보유는 `StockTicker` singleton, 동안 `StockTicker` 에 대 한 참조를 보유는 **IHubConnectionContext** 에 대 한는 `StockTickerHub`합니다. 이 인터페이스를 사용 하 여 통신할 수 `StockTickerHub` 인스턴스. (자세한 내용은 참조 [ASP.NET SignalR과 서버 브로드캐스트](index.md).)

이러한 종속성을 약간 정리 가능 여부는 IoC 컨테이너를 사용할 수 있습니다. 첫째, 보겠습니다 단순화는 `StockTickerHub` 및 `StockTicker` 클래스입니다. 다음 코드에서 I 한 주석으로 처리 파트는 필요 하지 않습니다.

매개 변수가 없는 생성자를 제거 `StockTicker`합니다. 대신 항상 DI 허브를 만들려면 사용 합니다.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

StockTicker, singleton 인스턴스를 제거 합니다. 이상에서는 IoC 컨테이너 StockTicker 수명을 제어 하려면 사용 합니다. 또한 생성자는 공용 확인 합니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다 다음으로, `StockTicker`합니다. 에서는이 인터페이스를 분리 하는 `StockTickerHub` 에서 `StockTicker` 클래스입니다.

Visual Studio에서는이 종류의 리팩터링 용이 합니다. StockTicker.cs 파일을 열고 마우스 오른쪽 단추로 클릭는 `StockTicker` 클래스를 선언 하 고 선택 **리팩터링** 중... **인터페이스 추출**합니다.

![](dependency-injection/_static/image1.png)

에 **인터페이스 추출** 대화 상자를 클릭 하 여 **모두 선택**합니다. 다른 기본값을 그대로 둡니다. **확인**을 클릭합니다.

![](dependency-injection/_static/image2.png)

Visual Studio 이라는 새 인터페이스를 만듭니다 `IStockTicker`, 변경 및 `StockTicker` 를 파생할 `IStockTicker`합니다.

IStockTicker.cs 파일을 열고 변경 하는 인터페이스 **공용**합니다.

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

에 `StockTickerHub` 클래스의 두 인스턴스를 변경, `StockTicker` 를 `IStockTicker`:

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

만들기는 `IStockTicker` 인터페이스는 필수가 아니지만 DI 응용 프로그램의 구성 요소 간의 결합을 줄이는 데 유용한 방법을 보여 주려고 합니다.

## <a name="add-the-ninject-library"></a>Ninject 라이브러리 추가

.NET에 대 한 많은 오픈 소스 IoC 컨테이너 있습니다. 이 자습서에 대 한 사용 [Ninject](http://www.ninject.org/)합니다. (다른 인기 있는 라이브러리 포함 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), 및 [StructureMap ](http://docs.structuremap.net).)

NuGet 패키지 관리자 설치를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)합니다. Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자** | **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>SignalR의 종속성 확인자를 대체 합니다.

SignalR 내 Ninject를 사용 하려면에서 파생 되는 클래스를 만듭니다 **DefaultDependencyResolver**합니다.

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

이 클래스는 재정의 **GetService** 및 **GetServices** 방식의 **DefaultDependencyResolver**합니다. SignalR 허브 인스턴스는 SignalR에서 내부적으로 사용 하는 다양 한 서비스를 포함 하 여 런타임에 다양 한 개체를 만들 수 이러한 메서드를 호출 합니다.

- **GetService** 메서드는 형식의 단일 인스턴스를 만듭니다. 이 메서드를 호출 Ninject 커널 재정의 **TryGet** 메서드. 해당 메서드가 null을 반환 하는 경우 대신 기본 해결 프로그램.
- **GetServices** 메서드는 지정 된 형식의 개체의 컬렉션을 만듭니다. 기본 해결 프로그램에서 결과 함께 Ninject에서 결과 연결 하려면이 메서드를 재정의 합니다.

## <a name="configure-ninject-bindings"></a>Ninject 바인딩을 구성합니다

이제 Ninject 바인딩을 형식 선언에 사용 합니다.

RegisterHubs.cs 파일을 엽니다. 에 `RegisterHubs.Start` 메서드를 Ninject 호출 하는 Ninject 컨테이너 만들기는 *커널*합니다.

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

이 사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

에 대 한 바인딩을 만들 `IStockTicker` 다음과 같습니다.

[!code-html[Main](dependency-injection/samples/sample17.html)]

이 코드에 다음 두 가지 의미 합니다. 첫째, 응용 프로그램에서 필요할 때마다는 `IStockTicker`, 커널의 인스턴스를 만들도록 `StockTicker`합니다. 두 번째는 `StockTicker` 클래스를 단일 개체로 만든 이어야 합니다. Ninject는 개체의 인스턴스를 하나 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.

에 대 한 바인딩을 만들 **IHubConnectionContext** 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

이 코드 creatres 반환 하는 익명 함수는 **IHubConnection**합니다. **WhenInjectedInto** 메서드를 만들 때만이 함수를 사용 하는 Ninject 지시 `IStockTicker` 인스턴스. SignalR 만들어지는 이유는 **IHubConnectionContext** 인스턴스를 내부적으로 SignalR을 만드는 방법을 재정의를 만들 필요가 없습니다. 이 함수에만 적용 됩니다 우리의 `StockTicker` 클래스입니다.

종속성 확인자에 전달 된 **MapHubs** 메서드:

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

이제 SignalR은에 지정 된 확인자를 사용 하 여 **MapHubs**, 기본 해결 프로그램 대신 합니다.

다음은 대 한 전체 코드 `RegisterHubs.Start`합니다.

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 f5 키를 누릅니다. 브라우저 창에서 디렉터리로 이동 `http://localhost:*port*/SignalR.Sample/StockTicker.html`합니다.

![](dependency-injection/_static/image3.png)

응용 프로그램에 정확히 동일한 기능을 이전 합니다. (참조에 대 한 [ASP.NET SignalR과 서버 브로드캐스트](index.md).) 동작을 변경 하지 않은 했습니다. 방금 쉽게 코드 테스트, 유지 관리 및 개발할 수 있습니다.
