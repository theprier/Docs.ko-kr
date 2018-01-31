---
uid: web-api/overview/advanced/dependency-injection
title: "ASP.NET Web API 2의에서 종속성 주입 | Microsoft Docs"
author: MikeWasson
description: "이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성 주입 하는 방법을 보여 줍니다. 자습서 Web API 2 Unity 응용 프로그램 블록에 사용 되는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 7f64cc83e36c80b0ffd53edfc629557c0847b200
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2의에서 종속성 주입
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성 주입 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - [Unity 응용 프로그램 블록](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (버전 5도 작동)


## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

A *종속성* 는 다른 개체에 필요한 모든 개체. 정의에 공통적으로 적용 하는 예를 들어 한 [리포지토리](http://martinfowler.com/eaaCatalog/repository.html) 데이터 액세스를 처리 하는 합니다. 예를 설명 하겠습니다. 첫째, 도메인 모델을 정의 합니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Entity Framework를 사용 하 여 데이터베이스에서 항목을 저장 하는 간단한 저장소 클래스는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

이제 Web API 컨트롤러에 대 한 GET 요청을 지 원하는 정의 해보겠습니다 `Product` 엔터티. (I 맞추고 나머지 POST 및 간단한 설명을 위해 다른 방법입니다.) 다음은 첫 번째 시도가입니다.

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

컨트롤러 클래스에 의존 하는 `ProductRepository`, 만들 컨트롤러를 하도록 우리는 `ProductRepository` 인스턴스. 그러나 여러 가지 이유로 하드 코딩 이러한 방식으로 종속성 않는 것이 좋습니다가 있습니다.

- 바꾸려는 경우 `ProductRepository` 를 다른 구현으로도 수정 해야 컨트롤러 클래스입니다.
- 경우는 `ProductRepository` 종속성 컨트롤러 내을 구성 해야 합니다. 다중 컨트롤러가 있는 대규모 프로젝트에 대 한 구성 코드 프로젝트에 분산 됩니다.
- 있기 단위 테스트에 하드 컨트롤러 쿼리는 데이터베이스에 하드 코드 되어 있습니다. 단위 테스트에 대 한 두고 디자인 실행 불가능 한 모의 또는 스텁 리포지토리를 사용 해야 합니다.

이러한 문제를 해결 하기 *주입* 저장소 컨트롤러에 있습니다. 첫째, 리팩터링는 `ProductRepository` 인터페이스에는 클래스:

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

그런 다음 제공 된 `IProductRepository` 를 생성자 매개 변수로:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

이 예에서는 [생성자 삽입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다. 사용할 수도 있습니다 *setter 주입*setter 메서드 또는 속성을 통해 종속성을 설정한 합니다.

하지만 여기에 문제가 응용 프로그램 컨트롤러를 직접 만들 하지 않습니다. Web API 요청을 라우팅하기과 웹 API에 대 한 때 컨트롤러를 만듭니다 `IProductRepository`합니다. 이 경우에 Web API 종속성 확인자입니다.

## <a name="the-web-api-dependency-resolver"></a>Web API 종속성 확인자

Web API 정의 **되며 IDependencyResolver** 종속성을 확인 하기 위한 인터페이스입니다. 인터페이스의 정의 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope** 인터페이스에는 두 가지 방법:

- **GetService** 는 형식의 인스턴스를 만듭니다.
- **GetServices** 지정 된 형식의 개체의 컬렉션을 만듭니다.

**되며 IDependencyResolver** 메서드 상속 **IDependencyScope** 추가 **BeginScope** 메서드. 이 자습서의 뒷부분에 나오는 범위에 대 한 설명 하겠습니다.

첫 번째로 호출 Web API 컨트롤러 인스턴스를 만들 때 **IDependencyResolver.GetService**컨트롤러 종류에 전달 합니다. 모든 종속성을 확인할 컨트롤러를 만들려면이 확장성 후크를 사용할 수 있습니다. 경우 **GetService** null을 반환, Web API 컨트롤러 클래스에 매개 변수가 없는 생성자를 찾습니다.

## <a name="dependency-resolution-with-the-unity-container"></a>Unity 컨테이너와 종속성 확인

전체 작성할 수 있지만 **되며 IDependencyResolver** 인터페이스 처음부터이 구현은 웹 API 기존 IoC 컨테이너 사이의 연결 다리 역할을 실제로으로 설계 합니다.

IoC 컨테이너는 종속성을 관리 하는 소프트웨어 구성 요소입니다. 컨테이너 형식을 등록 하 고이 정보를 개체를 만들 컨테이너를 사용 합니다. 컨테이너는 종속성 관계를 자동으로 알아 합니다. 많은 IoC 컨테이너 개체 수명, 범위 등의 작업을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"은 "컨트롤의 inversion" 되는 일반적인 패턴을 설정 하는 응용 프로그램 코드에는 프레임 워크를 호출 하는 경우이 합니다. IoC 컨테이너 개체에 대 한 구문, 일반적인 제어 흐름을 "반전"입니다.


이 자습서에서는 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) Microsoft 패턴에서 &amp; 사례입니다. (다른 인기 있는 라이브러리 포함 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), 및 [StructureMap ](http://docs.structuremap.net/).) Unity를 설치 하려면 NuGet 패키지 관리자를 사용할 수 있습니다. **도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

여기에의 구현 **되며 IDependencyResolver** 를 래핑하는 Unity의 컨테이너입니다.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> 경우는 **GetService** 반환 해야 메서드 형식을 확인할 수 없습니다, **null**합니다. 경우는 **GetServices** 메서드 형식을 확인할 수 없습니다, 빈 컬렉션 개체를 반환 해야 합니다. 알 수 없는 형식에 대 한 예외를 throw 하지 마십시오.


## <a name="configuring-the-dependency-resolver"></a>종속성 확인자 구성

종속성 확인자에 설정 된 **DependencyResolver** 은 전역 **HttpConfiguration** 개체입니다.

다음 코드 레지스터는 `IProductRepository` Unity와 상호 작용 하 고 다음 만듭니다는 `UnityResolver`합니다.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>종속성 범위와 컨트롤러 수명

컨트롤러는 요청에 따라 생성 됩니다. 개체 수명 관리 하려면 **되며 IDependencyResolver** 의 개념을 사용 하는 *범위*합니다.

에 연결 된 종속성 확인자는 **HttpConfiguration** 개체에 전역 범위입니다. Web API 컨트롤러를 만들 때 호출 **BeginScope**합니다. 이 메서드는 반환 된 **IDependencyScope** 자식 범위를 나타내는입니다.

그런 다음 웹 API를 호출 **GetService** 컨트롤러를 만들를 자식 범위에 있습니다. Web API를 호출 하는 요청이 완료 되 면 **Dispose** 하위 범위에 있습니다. 사용 하 여는 **Dispose** 메서드를 컨트롤러의 종속성을 삭제 합니다.

구현 하는 방법은 **BeginScope** IoC 컨테이너에 따라 달라 집니다. Unity에 대 한 범위는 자식 컨테이너에 해당합니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

대부분의 IoC 컨테이너와 비슷한 해당 하는 경우
