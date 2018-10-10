---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2에서에서 종속성 주입 | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 주입 하는 방법을 보여줍니다. 자습서 웹 API 2 Unity Application Block에 사용 되는 소프트웨어 버전 중...
ms.author: riande
ms.date: 01/20/2014
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: c58b06af0044144cf28cc36c16a41672aa1f6eb3
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48911267"
---
<a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 종속성 주입
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 이 자습서에서는 ASP.NET Web API 컨트롤러에 종속성을 주입 하는 방법을 보여줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - [Unity Application Block](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (버전 5 에서도 작동)


## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

‘종속성’은 다른 개체에 필요한 모든 개체입니다. 예를 들어 정의에 공통적으로 적용 되는 [리포지토리](http://martinfowler.com/eaaCatalog/repository.html) 데이터 액세스를 처리 하는 합니다. 예를 들어 살펴보겠습니다. 첫째, 도메인 모델을 정의 합니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Entity Framework를 사용 하 여 데이터베이스에서 항목을 저장 하는 간단한 저장소 클래스는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

이제 Web API 컨트롤러에 대 한 GET 요청을 지를 정의 하겠습니다 `Product` 엔터티. (겠다 게시물 및 단순성에 대 한 다른 방법을.) 첫 번째 시도 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

컨트롤러 클래스에 따라 달라 집니다 `ProductRepository`를 만들 컨트롤러는 우리가 하는 `ProductRepository` 인스턴스. 그러나 여러 가지 이유로 이러한 방식으로 종속성 하드 코드 하는 것은입니다.

- 바꾸려는 경우 `ProductRepository` 를 다른 구현 해야 컨트롤러 클래스를 수정 합니다.
- 경우는 `ProductRepository` 종속성에 컨트롤러 내에서 구성 해야 합니다. 여러 컨트롤러를 사용 하 여 대규모 프로젝트에 대 한 구성 코드 프로젝트에 분산 됩니다.
- 하기 어렵습니다 단위 테스트, 컨트롤러 데이터베이스를 쿼리하고도 하드 코딩 되어 있습니다. 단위 테스트의 경우와 두고 디자인 가능 하지는 mock 또는 스텁 리포지토리를 사용 해야 합니다.

이러한 문제를 처리할 수 있었습니다 *삽입* 저장소 컨트롤러입니다. 첫째, 리팩터링는 `ProductRepository` 인터페이스 클래스:

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

제공 된 `IProductRepository` 생성자 매개 변수로:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

이 예제에서는 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)합니다. 사용할 수도 있습니다 *setter 주입*setter 메서드 또는 속성을 통해 종속성을 설정 합니다.

하지만 이제 문제가 있어 응용 프로그램 컨트롤러를 직접 만들지 않습니다. Web API 요청을 라우팅하고 Web API는 모든 것을 인식 하지 못합니다 때 컨트롤러를 만듭니다 `IProductRepository`합니다. Web API 종속성 확인자 제공 되는 위치입니다.

## <a name="the-web-api-dependency-resolver"></a>웹 API 종속성 확인자

웹 API를 정의 합니다 **IDependencyResolver** 종속성 확인에 대 한 인터페이스입니다. 인터페이스의 정의 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

합니다 **IDependencyScope** 인터페이스에 두 가지 방법이 있습니다.

- **GetService** 는 형식의 인스턴스를 만듭니다.
- **GetServices** 지정 된 형식의 개체의 컬렉션을 만듭니다.

합니다 **IDependencyResolver** 메서드를 상속 **IDependencyScope** 추가 합니다 **BeginScope** 메서드. 이 자습서의 뒷부분에서 범위에 대 한 이야기 하겠습니다.

Web API 컨트롤러 인스턴스를 만드는 경우 먼저 호출한 **IDependencyResolver.GetService**컨트롤러 형식에 전달 합니다. 모든 종속성을 확인할 컨트롤러를 만들려면이 확장성 후크를 사용할 수 있습니다. 하는 경우 **GetService** null을 반환, Web API 컨트롤러 클래스에 있는 매개 변수가 없는 생성자를 찾습니다.

## <a name="dependency-resolution-with-the-unity-container"></a>Unity 컨테이너를 사용 하 여 종속성 확인

전체를 작성할 수 있지만 **IDependencyResolver** Web API와 기존 IoC 컨테이너 간의 브리지 역할을 실제로부터 인터페이스를 구현 합니다.

IoC 컨테이너는 종속성을 관리 하는 일을 담당 하는 소프트웨어 구성 요소입니다. 컨테이너로 형식을 등록 하 고이 정보를 개체를 만드는 컨테이너를 사용 합니다. 컨테이너는 자동으로 종속성 관계를 파악합니다. 많은 IoC 컨테이너를 사용 하면 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"는 "제어 반전"에 대 한 일반적인 패턴을 설정 하는 프레임 워크 응용 프로그램 코드를 호출 하는 경우이 합니다. IoC 컨테이너 생성 개체를 "반전" 컨트롤의 일반적인 흐름입니다.


이 자습서에서는 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) 에서 Microsoft Patterns &amp; 사례입니다. (다른 인기 있는 라이브러리 포함 [Castle Windsor](http://www.castleproject.org/)를 [Spring.Net](http://www.springframework.net/)를 [Autofac](https://code.google.com/p/autofac/)를 [Ninject](http://www.ninject.org/), 및 [StructureMap ](http://docs.structuremap.net/).) Unity를 설치 하려면 NuGet 패키지 관리자를 사용할 수 있습니다. **도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

여기의 구현인 **IDependencyResolver** Unity 컨테이너를 래핑합니다.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> 경우는 **GetService** 메서드는 형식을 확인할 수 없습니다, 반환할 **null**합니다. 경우는 **GetServices** 메서드는 형식을 확인할 수 없습니다, 빈 컬렉션 개체를 반환 해야 합니다. 알 수 없는 형식에 대 한 예외를 throw 하지 마십시오.


## <a name="configuring-the-dependency-resolver"></a>종속성 확인자를 구성합니다.

종속성 확인자를 설정 합니다 **DependencyResolver** 은 전역 **HttpConfiguration** 개체입니다.

다음 코드는 등록 된 `IProductRepository` Unity를 사용 하 여 인터페이스를 만듭니다를 `UnityResolver`합니다.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>종속성 범위 및 컨트롤러 수명

컨트롤러는 요청에 따라 생성 됩니다. 개체 수명 관리 **IDependencyResolver** 개념을 사용 하는 *범위*합니다.

종속성 확인자에 연결 합니다 **HttpConfiguration** 개체에 전역 범위입니다. Web API 컨트롤러를 만들 때 호출한 **BeginScope**합니다. 이 메서드는 **IDependencyScope** 자식 범위를 나타내는입니다.

웹 API 호출 **GetService** 컨트롤러를 만들려면 자식 범위에 있습니다. Web API를 호출 하는 요청이 완료 되 면 **Dispose** 자식 범위에 있습니다. 사용 된 **Dispose** 컨트롤러의 종속성을 삭제 하는 방법입니다.

구현 하는 방법을 **BeginScope** IoC 컨테이너에 따라 달라 집니다. Unity에 대 한 범위는 자식 컨테이너에 해당 됩니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

대부분의 IoC 컨테이너에 유사한 상응 합니다.
