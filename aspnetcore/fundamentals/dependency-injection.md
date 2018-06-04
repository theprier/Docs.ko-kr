---
title: ASP.NET Core에서 종속성 주입
author: ardalis
description: ASP.NET Core에서 종속성 주입을 구현하는 방법 및 사용 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/dependency-injection
ms.openlocfilehash: 14c3d464773fe78a563a27776bfcd124c22df134
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34566960"
---
# <a name="dependency-injection-in-aspnet-core"></a>ASP.NET Core에서 종속성 주입

<a name="fundamentals-dependency-injection"></a>

작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)

ASP.NET Core는 처음부터 종속성 주입을 지원 및 활용하도록 설계되었습니다. ASP.NET Core 응용 프로그램은 기본 제공 프레임워크 서비스를 시작 클래스의 메서드에 주입하여 활용할 수 있으며, 응용 프로그램 서비스도 주입에 대해 구성할 수 있습니다. ASP.NET Core에서 제공되는 기본 서비스 컨테이너는 최소한의 기능 집합을 제공하며 다른 컨테이너를 대체하는 데 사용할 수 없습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-is-dependency-injection"></a>종속성 주입이란?

DI(종속성 주입)란 개체와 협력자 또는 종속성 간의 느슨한 결합을 실현하기 위한 기술입니다. 직접 협력자를 인스턴스화하거나 정적 참조를 사용하는 대신에, 해당 작업을 수행하기 위해 필요한 클래스의 개체가 특정 방식으로 클래스에 제공됩니다. 대부분의 경우 클래스는 해당 생성자를 통해 해당 종속성을 선언하게 되며 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따르도록 허용합니다. 이 방법을 “생성자 주입”이라고 합니다.

DI를 염두에 두고 클래스를 설계한 경우 협력자에게 직접적으로 하드 코드된 종속성이 없기 때문에 더 느슨하게 결합됩니다. 이는 *“높은 수준의 모듈은 낮은 수준의 모듈에 의존해서는 안되며 둘다 추상화에 의존해야 한다”* 는 [종속성 반전 원칙](http://deviq.com/dependency-inversion-principle/)을 따릅니다. 클래스는 특정 구현을 참조하는 대신, 클래스를 생성할 때에 제공되는 추상화(일반적으로 `interfaces`)를 요청합니다. 인터페이스로 종속성을 추출하고 매개 변수로 이러한 인터페이스의 구현을 제공하는 것 또한 [전략 디자인 패턴](http://deviq.com/strategy-design-pattern/)의 예시입니다.

시스템이 DI를 사용하도록 설계된 경우, 해당 생성자(또는 속성)를 통해 해당 종속성을 요청하는 많은 클래스를 사용하면 클래스가 연결된 종속성으로 이러한 클래스를 만들도록 하는 데 유용합니다. 이러한 클래스를 *컨테이너* 또는 더 구체적으로 [IoC(Inversion of Control)](http://deviq.com/inversion-of-control/) DI(종속성 주입) 컨테이너라고 합니다. 컨테이너는 본질적으로 요청된 유형의 인스턴스를 제공해야 하는 팩터리입니다. 지정된 유형에 종속성이 있음이 선언되고, 컨테이너가 종속성 유형을 제공하도록 구성된 경우, 요청된 인스턴스 생성의 일환으로 종속성이 만들어집니다. 이러한 방식에서는 모든 하드 코드된 개체를 생성할 필요 없이 복잡한 종속성 그래프가 클래스에 제공될 수 있습니다. 해당 종속성이 있는 개체를 만드는 것 외에도 컨테이너는 일반적으로 응용 프로그램 내 개체 수명 주기를 관리합니다.

ASP.NET Core에는 생성자 주입을 기본으로 지원하는 간단한 기본 제공 컨테이너(`IServiceProvider` 인터페이스에서 interface)가 포함되며, ASP.NET을 사용하면 DI를 통해 특정 서비스를 사용할 수 있습니다. ASP.NET의 컨테이너는 *서비스*로 관리하는 유형을 나타냅니다. 이 문서의 나머지 부분에서 *서비스*는 ASP.NET Core의 IoC 컨테이너에서 관리하는 유형을 나타냅니다. 응용 프로그램의 `Startup` 클래스에 있는 `ConfigureServices` 메서드에서 기본 제공 컨테이너의 서비스를 구성합니다.

> [!NOTE]
> Martin Fowler는 [Inversion of Control 컨테이너 및 종속성 주입 패턴](https://www.martinfowler.com/articles/injection.html)에 대한 광범위한 문서를 작성했습니다. Microsoft Patterns and Practices에도 [종속성 주입](https://msdn.microsoft.com/library/hh323705.aspx)에 대한 훌륭한 설명이 있습니다.

> [!NOTE]
> 이 문서에서는 모든 ASP.NET 응용 프로그램에 적용되는 종속성 주입을 설명합니다. MVC 컨트롤러 내 종속성 주입은 [종속성 주입 및 컨트롤러](../mvc/controllers/dependency-injection.md)에서 다룹니다.

### <a name="constructor-injection-behavior"></a>생성자 주입 동작

생성자 주입을 위해서는 문제의 생성자가 *public*이어야 합니다. 그렇지 않으면 앱은 `InvalidOperationException`을 throw하게 됩니다.

> ‘YourType’ 유형에 대한 적합한 생성자를 찾을 수 없습니다. 유형이 구체적이고 서비스가 public 생성자의 모든 매개 변수에 등록되었는지 확인합니다.

생성자 주입을 위해서는 적합한 생성자가 하나만 있어야 합니다. 생성자 오버로드가 지원되지만, 해당 인수가 모두 종속성 주입으로 처리될 수 있는 하나의 오버로드만 존재할 수 있습니다. 둘 이상인 경우 앱은 `InvalidOperationException`을 throw하게 됩니다.

> 지정된 모든 인수 형식을 수락하는 여러 명의 생성자를 ‘YourType’ 유형에서 찾았습니다. 적용 가능한 생성자는 하나여야 합니다.

생성자는 종속성 주입으로 제공되지 않은 인수를 수락할 수 있지만, 기본값을 지원해야 합니다. 예:

```csharp
// throws InvalidOperationException: Unable to resolve service for type 'System.String'...
public CharactersController(ICharacterRepository characterRepository, string title)
{
    _characterRepository = characterRepository;
    _title = title;
}

// runs without error
public CharactersController(ICharacterRepository characterRepository, string title = "Characters")
{
    _characterRepository = characterRepository;
    _title = title;
}
```

## <a name="using-framework-provided-services"></a>프레임워크에서 제공한 서비스 사용

`Startup` 클래스의 `ConfigureServices` 메서드는 응용 프로그램이 사용하는 서비스를 정의하는 작업을 담당하며, Entity Framework Core 및 ASP.NET Core MVC와 같은 플랫폼 기능을 포함합니다. 처음에 `ConfigureServices`에 제공된 `IServiceCollection`에는 정의된 다음과 같은 서비스가 있습니다([호스트 구성 방법](xref:fundamentals/host/index)에 따라).

| 서비스 종류 | 수명 |
| ----- | ------- |
| [Microsoft.AspNetCore.Hosting.IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) | Singleton |
| [Microsoft.Extensions.Logging.ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory) | Singleton |
| [Microsoft.Extensions.Logging.ILogger&lt;T&gt;](/dotnet/api/microsoft.extensions.logging.ilogger) | Singleton |
| [Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory](/dotnet/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | Transient |
| [Microsoft.AspNetCore.Http.IHttpContextFactory](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextfactory) | Transient |
| [Microsoft.Extensions.Options.IOptions&lt;T&gt;](/dotnet/api/microsoft.extensions.options.ioptions-1) | Singleton |
| [System.Diagnostics.DiagnosticSource](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | Singleton |
| [System.Diagnostics.DiagnosticListener](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | Singleton |
| [Microsoft.AspNetCore.Hosting.IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) | Transient |
| [Microsoft.Extensions.ObjectPool.ObjectPoolProvider](/dotnet/api/microsoft.extensions.objectpool.objectpoolprovider) | Singleton |
| [Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) | Transient |
| [Microsoft.AspNetCore.Hosting.Server.IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) | Singleton |
| [Microsoft.AspNetCore.Hosting.IStartup](/dotnet/api/microsoft.aspnetcore.hosting.istartup) | Singleton |
| [Microsoft.AspNetCore.Hosting.IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | Singleton |

다음은 `AddDbContext`, `AddIdentity` 및 `AddMvc`와 같은 다양한 확장 메서드를 사용하여 추가 서비스를 컨테이너에 추가하는 방법에 대한 예시입니다.

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

MVC와 같이 ASP.NET에서 제공하는 기능 및 미들웨어는 단일 Add*ServiceName* 확장 메서드 사용에 대한 규칙에 따라 해당 기능에 필요한 모든 서비스를 등록합니다.

> [!TIP]
> 해당 매개 변수 목록을 통해 `Startup` 메서드 내에서 특정 프레임워크에서 제공한 서비스를 요청할 수 있습니다. 자세한 내용은 [응용 프로그램 시작](startup.md)을 참조하세요.

## <a name="registering-services"></a>서비스 등록

다음과 같이 사용자 고유의 응용 프로그램 서비스를 등록할 수 있습니다. 첫 번째 제네릭 형식은 컨테이너에서 요청되는 형식(일반적으로 인터페이스)을 나타냅니다. 두 번째 제네릭 형식은 컨테이너에 의해 인스턴스화되고 그러한 요청을 처리하는 데 사용되는 구체적 형식을 나타냅니다.

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> 각 `services.Add<ServiceName>` 확장 메서드는 서비스를 추가(및 잠재적으로 구성)합니다. 예를 들어 `services.AddMvc()`는 MVC에서 요청하는 서비스를 추가합니다. 이 규칙에 따라 `Microsoft.Extensions.DependencyInjection` 네임스페이스의 확장 메서드를 배치하여 서비스 등록의 그룹을 캡슐화하는 것이 좋습니다.

`AddTransient` 메서드는 추상 형식을 매핑하는 데 사용되어, 이를 요청하는 모든 개체에서 별도로 인스턴스화되는 서비스를 구체화합니다. 이를 서비스의 *수명*이라고 하며, 추가 수명 옵션은 다음과 같습니다. 등록하는 서비스마다 적절한 수명을 선택하는 것이 중요합니다. 요청한 각 클래스에 서비스의 새 인스턴스를 제공해야 하나요? 지정된 웹 요청에 하나의 인스턴스만 사용해야 하나요? 또는 응용 프로그램의 수명 동안 단일 인스턴스를 사용해야 하나요?

이 문서에 대한 샘플에서는 `CharactersController`라는 문자 이름을 표시하는 간단한 컨트롤러가 나옵니다. 해당 `Index` 메서드는 응용 프로그램에 저장된 문자의 현재 목록을 표시하고, 없는 경우 소수의 문자를 사용하여 컬렉션을 초기화합니다. 이 응용 프로그램이 지속성을 위해 Entity Framework Core 및 `ApplicationDbContext` 클래스를 사용하긴 하지만 컨트롤러에는 해당 항목이 없습니다. 대신, 특정 데이터 액세스 메커니즘은 [리포지토리 패턴](http://deviq.com/repository-pattern/)을 따르는 인터페이스 `ICharacterRepository` 뒤에서 추상화되었습니다. `ICharacterRepository`의 인스턴스는 생성자에 의해 요청되고 전용 필드에 할당됩니다. 그런 다음, 필요에 따라 문자에 액세스하는 데 사용됩니다.

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

`ICharacterRepository`는 컨트롤러가 `Character` 인스턴스를 사용해야 하는 두 가지 메서드를 정의합니다.

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

이 인터페이스는 런타임에 사용되는 구체적인 형식인 `CharacterRepository`에 의해 차례로 구현됩니다.

> [!NOTE]
> `CharacterRepository` 클래스와 함께 사용되는 DI 방식은 “리포지토리”나 데이터 액세스 클래스뿐 아니라 모든 응용 프로그램 서비스에 대해 따를 수 있는 일반 모델입니다.

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

`CharacterRepository`는 해당 생성자에서 `ApplicationDbContext`를 요청합니다. 종속성 주입이 자체 종속성을 차례로 요청하는 요청된 각 종속성을 통해 이와 같이 연결된 방식으로 사용되는 것은 드문 일이 아닙니다. 컨테이너는 그래프의 모든 종속성을 해결하고, 완전히 해결된 서비스를 반환하는 작업을 담당합니다.

> [!NOTE]
> 요청된 개체 및 거기에 필요한 모든 개체를 만드는 것을 경우에 따라 *개체 그래프*라고 합니다. 마찬가지로, 해결해야 하는 종속성이 모인 집합은 일반적으로 *종속성 트리* 또는 *종속성 그래프*라고 합니다.

이 경우 `ICharacterRepository`와 `ApplicationDbContext`는 모두 차례로 `Startup`에서 `ConfigureServices`의 서비스 컨테이너에 등록해야 합니다. `ApplicationDbContext`는 확장 메서드 `AddDbContext<T>`에 대한 호출로 구성됩니다. 다음 코드에서는 `CharacterRepository` 형식의 등록을 보여 줍니다.

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

Entity Framework 컨텍스트는 `Scoped` 수명을 사용하여 서비스 컨테이너에 추가해야 합니다. 이는 위와 같이 도우미 메서드를 사용할 경우 자동으로 처리됩니다. Entity Framework를 사용하게 되는 리포지토리는 동일한 수명을 사용해야 합니다.

> [!WARNING]
> 경계해야 할 주요 위험은 Singleton의 `Scoped` 서비스를 해결하는 것입니다. 그러한 경우 후속 요청을 처리할 때 서비스가 잘못된 상태일 가능성이 있습니다.

종속성이 있는 서비스는 컨테이너에 종속성을 등록해야 합니다. 서비스의 생성자에게 `string`과 같은 기본 형식이 필요한 경우 [구성](xref:fundamentals/configuration/index) 및 [옵션 패턴](xref:fundamentals/configuration/options)을 사용하여 주입할 수 있습니다.

## <a name="service-lifetimes-and-registration-options"></a>서비스 수명 및 등록 옵션

ASP.NET 서비스는 다음 수명을 사용하여 구성할 수 있습니다.

**Transient**

Transient 수명 서비스는 요청할 때마다 만들어집니다. 이 수명은 간단한 상태 비저장 서비스에 가장 적합합니다.

**Scoped**

Scoped 수명 서비스는 요청당 한 번만 만들어집니다.

> [!WARNING]
> 미들웨어에서 범위가 지정된 서비스를 사용하는 경우 `Invoke` 또는 `InvokeAsync` 메서드에 서비스를 삽입합니다. 생성자 삽입은 서비스가 싱글톤처럼 작동하게 하므로 이러한 방법으로 삽입하지 마세요.

**Singleton**

Singleton 수명 서비스는 처음 요청할 때 만들어집니다(또는 인스턴스를 지정한 경우 `ConfigureServices`가 실행될 때). 그런 다음, 모든 후속 요청이 동일한 인스턴스를 사용하게 됩니다. 응용 프로그램에 Singleton 동작이 필요한 경우, 자체 클래스에서 Singleton 디자인 패턴을 구현하고 사용자 개체의 수명을 관리하는 대신 서비스 컨테이너가 서비스의 수명을 관리하도록 허용하는 것이 좋습니다.

서비스는 여러 방법으로 컨테이너에 등록할 수 있습니다. 앞에서 우리는 사용할 구체적인 형식을 지정하여 주어진 형식으로 서비스 구현을 등록하는 방법을 살펴보았습니다. 또한 요청에 따라 인스턴스를 만드는 데 사용되도록 팩터리를 지정할 수 있습니다. 세 번째 방법은 사용할 형식의 인스턴스를 직접 지정하는 것입니다. 이 경우 컨테이너는 인스턴스 생성을 시도하지 않습니다(인스턴스를 제거하지도 않음).

이러한 수명 및 등록 옵션 간의 차이점을 살펴보려면 하나 이상의 작업을 고유한 ID인 `OperationId`가 있는 *operation*으로 나타내는 간단한 인터페이스를 고려해 보세요. 이 서비스에 대한 수명을 구성하는 방법에 따라 컨테이너는 클래스 요청에 동일하거나 다른 서비스 인스턴스를 제공합니다. 어떤 수명이 요청되었는지 명확히 하기 위해 수명 옵션당 하나의 형식만 만듭니다.

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

해당 생성자에서 `Guid`를 수락하거나, 아무것도 제공되지 않은 경우 새로운 `Guid`를 사용하는, 단일 클래스 `Operation`을 사용하여 이러한 인터페이스를 구현합니다.

다음으로 `ConfigureServices`에서 각 형식이 명명된 수명에 따라 컨테이너에 추가됩니다.

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

`IOperationSingletonInstance` 서비스가 `Guid.Empty`의 알려진 ID의 특정 인스턴스를 사용 중이므로 이 형식을 언제 사용하는지 명확해집니다(해당 Guid는 모두 0이 됨). 또한 `Operation` 형식을 서로 종속하는 `OperationService`를 등록했으므로 이 서비스가 각 작업 형식에 대한 컨트롤러로 동일한 인스턴스를 가져오는지, 아니면 새로운 인스턴스를 가져오는지 여부가 요청 내에서 명확해집니다. 이 서비스는 모두 해당 종속성을 속성으로 노출하므로 보기에 표시할 수 있습니다.

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

응용 프로그램에 대한 서로 다른 개별 요청 내 및 요청 간 개체 수명을 보여 주기 위해 샘플에는 `OperationService` 뿐만 아니라 각 `IOperation` 형식 종류를 요청하는 `OperationsController`가 포함되어 있습니다. 그런 다음, `Index` 작업은 모든 컨트롤러 및 서비스의 `OperationId` 값을 표시합니다.

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

이제 두 개의 개별 요청이 이 컨트롤러 작업에서 수행됩니다.

![첫 번째 요청의 Transient, Scoped, Singleton에 대한 작업 ID 값(GUID), 인스턴스 컨트롤러 및 작업 서비스 작업을 표시하는 Microsoft Edge에서 실행되는 종속성 주입 샘플 웹 응용 프로그램의 작업 보기](dependency-injection/_static/lifetimes_request1.png)

![두 번째 요청의 작업 ID 값을 표시하는 작업 보기.](dependency-injection/_static/lifetimes_request2.png)

어떤 `OperationId` 값이 요청 내 및 요청 간 달라지는지 확인합니다.

* *Transient* 개체는 항상 다릅니다. 새 인스턴스가 모든 컨트롤러 및 모든 서비스에 제공됩니다.

* *Scoped* 개체는 요청 내에서는 동일하지만 다른 요청에서는 다릅니다.

* *Singleton* 개체는 모든 개체 및 모든 요청에 대해 동일합니다(`ConfigureServices`에 인스턴스 제공 여부에 관계 없이).

## <a name="resolve-a-scoped-service-within-the-application-scope"></a>응용 프로그램 범위 내에서 범위가 지정된 서비스 확인

[IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope)와 함께 [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope)를 만들어 앱 범위 내에서 범위가 지정된 서비스를 확인합니다. 이 방법은 시작 시 범위가 지정된 서비스에 액세스하여 초기화 작업을 실행하는 데 유용합니다. 다음 예제에서는 `Program.Main`에서 `MyScopedService`에 대한 컨텍스트를 가져오는 방법을 보여 줍니다.

```csharp
public static void Main(string[] args)
{
    var host = BuildWebHost(args);

    using (var serviceScope = host.Services.CreateScope())
    {
        var services = serviceScope.ServiceProvider;

        try
        {
            var serviceContext = services.GetRequiredService<MyScopedService>();
            // Use the context here
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred.");
        }
    }

    host.Run();
}
```

## <a name="scope-validation"></a>범위 유효성 검사

앱이 ASP.NET Core 2.0 이상의 개발 환경에서 실행 중인 경우 기본 서비스 공급자가 다음을 확인하는 검사를 수행합니다.

* 범위가 지정된 서비스는 루트 서비스 공급자를 통해 간접적 또는 직접으로 확인되지 않습니다.
* 범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.

루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다. 루트 서비스 공급자의 수명은 공급자가 앱과 함께 시작되고 앱이 종료될 때 삭제되는 앱/서버의 수명에 해당합니다.

범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다. 범위가 지정된 서비스가 루트 컨테이너에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다. 서비스 범위의 유효성 검사는 `BuildServiceProvider`가 호출될 경우 이러한 상황을 catch합니다.

자세한 내용은 [웹 호스트의 범위 유효성 검사 항목](xref:fundamentals/host/web-host#scope-validation)을 참조하세요.

## <a name="request-services"></a>요청 서비스

`HttpContext`의 ASP.NET 요청 내에서 사용할 수 있는 서비스는 `RequestServices` 컬렉션을 통해 노출됩니다.

![요청 서비스가 요청의 서비스 컨테이너에 대한 액세스를 제공하는 IServiceProvider를 가져오거나 설정했다는 HttpContext 요청 서비스 Intellisense 상황별 대화 상자](dependency-injection/_static/request-services.png)

요청 서비스는 사용자가 응용 프로그램의 일부로 구성 및 요청한 서비스를 나타냅니다. 개체가 종속성을 지정한 경우에는 `ApplicationServices`가 아닌 `RequestServices`에 있는 형식으로 충족됩니다.

일반적으로 이러한 속성을 직접 사용해서는 안 됩니다. 대신 클래스의 생성자를 통해 요청한 클래스 형식을 요청하고 프레임워크에서 이러한 종속성을 주입하도록 해야 합니다. 이는 더 쉽게 테스트할 수 있고([테스트 및 디버그](xref:test/index) 참조) 더 느슨하게 결합되는 클래스를 일시 중단합니다.

> [!NOTE]
> `RequestServices` 컬렉션에 액세스하는 것보다 생성자 매개 변수로 종속성을 요청하는 것을 선호합니다.

## <a name="designing-services-for-dependency-injection"></a>종속성 주입을 위한 서비스 디자인

종속성 주입을 사용하여 자신의 협력자를 가져오도록 서비스를 디자인해야 합니다. 즉, 서비스 내에서 상태 저장 정적 메서드 호출 사용([정적 집착](http://deviq.com/static-cling/)이라고 알려진 코드 스멜을 야기) 및 종속 클래스의 직접 인스턴스화를 방지합니다. 형식을 인스턴스화할지 아니면 종속성 주입을 통해 요청할 것인지를 선택할 때 [New is Glue](https://ardalis.com/new-is-glue)라는 문구를 기억하는 것이 도움이 될 수 있습니다. [개체 지향 디자인의 SOLID 원칙](http://deviq.com/solid/)에 따라 클래스는 당연히 작고 잘 구성되며 쉽게 테스트됩니다.

클래스에 주입해야 할 종속성이 너무 많다면 어떻게 될까요? 이는 일반적으로 클래스가 너무 많은 작업을 시도하고 있으며 아마도 SRP([단일 책임 원칙](http://deviq.com/single-responsibility-principle/))를 위반하고 있다는 신호입니다. 해당 책임 몇 가지를 새로운 클래스로 이동하여 클래스를 리팩터링할 수 있는지 살펴 보세요. `Controller` 클래스는 UI 고려 사항에 집중해야 하므로, 비즈니스 규칙 및 데이터 액세스 구현 세부 정보는 이러한 [개별 고려 사항](http://deviq.com/separation-of-concerns/)에 적합한 클래스에 유지되어야 한다는 점을 기억하세요.

특히 데이터 액세스와 관련하여 `DbContext`를 컨트롤러에 주입할 수 있습니다(EF를 `ConfigureServices`의 서비스 컨테이너에 추가했다고 가정). 일부 개발자는 `DbContext`를 직접 주입하는 대신 데이터베이스에 리포지토리 인터페이스를 사용하는 것을 선호합니다. 인터페이스를 사용하여 데이터 액세스 논리를 한 곳으로 캡슐화하면 데이터베이스가 변경될 때 변경해야 하는 장소 수를 최소화할 수 있습니다.

### <a name="disposing-of-services"></a>서비스 해제

컨테이너는 만든 `IDisposable` 형식에 대해 `Dispose`를 호출합니다. 그러나 인스턴스를 컨테이너에 직접 추가하는 경우에는 삭제되지 않습니다.

예제:

```csharp
// Services implement IDisposable:
public class Service1 : IDisposable {}
public class Service2 : IDisposable {}
public class Service3 : IDisposable {}

public interface ISomeService {}
public class SomeServiceImplementation : ISomeService, IDisposable {}


public void ConfigureServices(IServiceCollection services)
{
    // container will create the instance(s) of these types and will dispose them
    services.AddScoped<Service1>();
    services.AddSingleton<Service2>();
    services.AddSingleton<ISomeService>(sp => new SomeServiceImplementation());

    // container didn't create instance so it will NOT dispose it
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

> [!NOTE]
> 버전 1.0에서 컨테이너는 만들지 않은 개체를 포함한 *모든* `IDisposable` 개체에서 dispose를 호출했습니다.

## <a name="replacing-the-default-services-container"></a>기본 서비스 컨테이너 대체

기본 제공 서비스 컨테이너는 프레임워크의 기본 조건 및 이를 기반으로 구성된 대부분의 소비자 응용 프로그램을 제공하는 것을 의미합니다. 그러나 개발자는 기본 제공 컨테이너를 선호하는 컨테이너로 바꿀 수 있습니다. `ConfigureServices` 메서드는 일반적으로 `void`를 반환하지만, 해당 시그니처가 변경되어 `IServiceProvider`를 반환하는 경우 다른 컨테이너를 구성하거나 반환할 수 있습니다. .NET에서 사용 가능한 많은 IOC 컨테이너가 있습니다. 이 예제에서는 [Autofac](https://autofac.org/) 패키지를 사용합니다.

먼저, 적절한 컨테이너 패키지를 설치합니다.

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

그런 다음, 컨테이너를 `ConfigureServices`에 구성하고 `IServiceProvider`를 반환합니다.

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // Add other framework services

    // Add Autofac
    var containerBuilder = new ContainerBuilder();
    containerBuilder.RegisterModule<DefaultModule>();
    containerBuilder.Populate(services);
    var container = containerBuilder.Build();
    return new AutofacServiceProvider(container);
}
```

> [!NOTE]
> 타사 DI 컨테이너를 사용하는 경우 `void` 대신 `IServiceProvider`를 반환하도록 `ConfigureServices`를 변경해야 합니다.

마지막으로 `DefaultModule`에서 Autofac을 정상적으로 구성합니다.

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

런타임 시 형식을 확인하고 종속성을 주입하는 데 Autofac이 사용됩니다. [Autofac 및 ASP.NET Core를 사용하는 방법에 대해 자세히 알아보세요](http://docs.autofac.org/en/latest/integration/aspnetcore.html).

### <a name="thread-safety"></a>스레드로부터의 안전성

Singleton 서비스는 스레드로부터 안전해야 합니다. Singleton 서비스가 Transient 서비스에 대한 종속성을 갖는 경우 Transient 서비스는 Singleton에서 사용되는 방식에 따라 스레드로부터 안전해야 할 수도 있습니다.

## <a name="recommendations"></a>권장 사항

종속성 주입을 사용할 때는 다음 권장 사항을 염두에 둬야 합니다.

* DI는 복잡한 종속성이 있는 개체입니다. 컨트롤러, 서비스, 어댑터 및 리포지토리는 모두 DI에 추가할 수도 있는 개체의 예입니다.

* 데이터 및 구성을 DI에 직접 저장하지 마십시오. 예를 들어 사용자의 쇼핑 카트는 일반적으로 서비스 컨테이너에 추가하지 말아야 합니다. 구성은 [옵션 패턴](xref:fundamentals/configuration/options)을 사용해야 합니다. 마찬가지로 다른 일부 개체에 대한 액세스를 허용하기 위해서만 존재하는 “데이터 보유자” 개체를 사용하지 마십시오. 가능한 경우 DI를 통해 필요한 실제 항목을 요청하는 것이 좋습니다.

* 서비스에 정적 액세스를 사용하지 마십시오.

* 응용 프로그램 코드에서 서비스 위치를 사용하지 마십시오.

* `HttpContext`에 정적 액세스를 사용하지 마십시오.

모든 권장 사항과 마찬가지로, 하나를 무시해야 하는 상황이 발생할 수 있습니다. 예외는 드물었습니다. 대부분 매우 특별한 사례는 프레임워크 자체 내에 있습니다.

종속성 주입은 정적/전역 개체 액세스 패턴의 *대안*입니다. 고정 개체 액세스와 함께 사용할 경우 DI의 장점을 실현할 수 없습니다.

## <a name="additional-resources"></a>추가 자료

* [뷰에 종속성 주입](xref:mvc/views/dependency-injection)
* [컨트롤러에 종속성 주입](xref:mvc/controllers/dependency-injection)
* [요구 사항 처리기의 종속성 주입](xref:security/authorization/dependencyinjection)
* [응용 프로그램 시작](xref:fundamentals/startup)
* [테스트 및 디버그](xref:test/index)
* [팩터리 기반 미들웨어 활성화](xref:fundamentals/middleware/extensibility)
* [종속성 주입으로 ASP.NET Core에 정리 코드 작성(MSDN)](https://msdn.microsoft.com/magazine/mt703433.aspx)
* [컨테이너 관리 응용 프로그램 디자인, 서막: 컨테이너는 어디에 속합니까?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)
* [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)
* [Inversion of Control 컨테이너 및 종속성 주입 패턴](https://www.martinfowler.com/articles/injection.html)(Fowler)
