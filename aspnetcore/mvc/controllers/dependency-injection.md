---
title: ASP.NET Core의 컨트롤러에 종속성 주입
author: ardalis
description: ASP.NET Core MVC 컨트롤러가 ASP.NET Core의 종속성 주입을 사용하여 해당 생성자를 통해 명시적으로 해당 종속성을 요청하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: mvc/controllers/dependency-injection
ms.openlocfilehash: 12247dbbbb6de3f8feb7bc37caec4ecf4bd21719
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206344"
---
# <a name="dependency-injection-into-controllers-in-aspnet-core"></a>ASP.NET Core의 컨트롤러에 종속성 주입

<a name="dependency-injection-controllers"></a>

작성자: [Steve Smith](https://ardalis.com/)

ASP.NET Core MVC 컨트롤러는 해당 생성자를 통해 명시적으로 해당 종속성을 요청해야 합니다. 경우에 따라 개별 컨트롤러 작업에는 서비스가 필요할 수 있으며, 컨트롤러 수준에서 요청하지 못할 수 있습니다. 이 경우에 작업 메서드의 매개 변수로 서비스를 주입할 수도 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample)([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="dependency-injection"></a>종속성 주입

종속성 주입은 [종속성 반전 원칙](http://deviq.com/dependency-inversion-principle/)을 따르는 기술로, 응용 프로그램을 느슨하게 결합된 모듈로 구성할 수 있습니다. ASP.NET Core는 [종속성 주입](../../fundamentals/dependency-injection.md)을 기본적으로 지원하므로 응용 프로그램을 더 쉽게 테스트하고 유지 관리할 수 있습니다.

## <a name="constructor-injection"></a>생성자 주입

생성자 기반 종속성 주입을 위한 ASP.NET Core의 기본 지원은 MVC 컨트롤러까지 확장합니다. 컨트롤러에 서비스 형식을 생성자 매개 변수로 추가하기만 하면 ASP.NET Core는 서비스 컨테이너의 기본 기능을 사용하여 해당 형식을 확인하려고 시도합니다. 서비스는 항상 그렇지는 않지만 일반적으로 인터페이스를 사용하여 정의됩니다. 예를 들어 현재 시간에 따라 달라지는 비즈니스 논리가 응용 프로그램에 있는 경우, 설정된 시간을 사용하는 구현에서 테스트가 통과될 수 있도록 시간을 검색하는(하드코딩이 아님) 서비스를 주입할 수 있습니다.

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Interfaces/IDateTime.cs)]


런타임 시 시스템 클록을 사용하도록 이와 같은 인터페이스를 구현하는 것은 매우 간단합니다.

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Services/SystemDateTime.cs)]


준비된 이 항목을 통해 컨트롤러에서 서비스를 사용할 수 있습니다. 이 경우 시간에 따라 사용자에게 인사말을 표시하도록 일부 논리를 `HomeController` `Index` 메서드에 추가하였습니다.

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=8,10,12,17,18,19,20,21,22,23,24,25,26,27,28,29,30&range=1-31,51-52)]

지금 응용 프로그램을 실행하는 경우 오류가 발생할 가능성이 있습니다.

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Unable to resolve service for type 'ControllerDI.Interfaces.IDateTime' while attempting to activate 'ControllerDI.Controllers.HomeController'.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.GetService(IServiceProvider sp, Type type, Type requiredBy, Boolean isDefaultParameterRequired)
```

이 오류는 `Startup` 클래스의 `ConfigureServices` 메서드에서 서비스를 구성하지 않은 경우에 발생합니다. `IDateTime`에 대한 요청이 `SystemDateTime`의 인스턴스를 사용하여 확인되도록 지정하려면 아래 목록에서 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=4&range=26-27,42-44)]

> [!NOTE]
> 이 특정 서비스는 여러 가지 다른 수명 옵션 중 하나를 사용하여 구현할 수 있습니다(`Transient`, `Scoped` 또는 `Singleton`). 각 범위 옵션이 서비스의 동작에 미치는 영향을 이해하려면 [종속성 주입](../../fundamentals/dependency-injection.md)을 참조하세요.

서비스를 한 번 구성하면 응용 프로그램을 실행하고 홈 페이지로 이동할 때 시간 기반 메시지가 예상대로 표시되어야 합니다.

![서버 인사말](dependency-injection/_static/server-greeting.png)

>[!TIP]
> 컨트롤러에서 종속성 [http://deviq.com/explicit-dependencies-principle/](http://deviq.com/explicit-dependencies-principle/)을 명시적으로 요청하여 코드를 더 쉽게 테스트할 수 있는 방법을 알아보려면 [컨트롤러 논리 테스트](testing.md)를 참조하세요.

ASP.NET Core의 기본 제공 종속성 주입은 클래스 요청 서비스에 대해 단일 생성자만 있어야 합니다. 생성자가 둘 이상인 경우 다음과 같은 예외가 나타날 수 있습니다.

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Multiple constructors accepting all given argument types have been found in type 'ControllerDI.Controllers.HomeController'. There should only be one applicable constructor.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.FindApplicableConstructor(Type instanceType, Type[] argumentTypes, ConstructorInfo& matchingConstructor, Nullable`1[]& parameterMap)
```

오류 메시지에 나타난 대로 단일 생성자를 사용하여 이 문제를 해결할 수 있습니다. 또한 [기본 종속성 주입 컨테이너를 타사 구현으로 대체](xref:fundamentals/dependency-injection#default-service-container-replacement)할 수 있습니다. 다수는 여러 생성자를 지원합니다.

## <a name="action-injection-with-fromservices"></a>FromServices로 작업 삽입

경우에 따라 컨트롤러 내에서 둘 이상의 작업에 서비스가 필요하지 않습니다. 이 경우 서비스를 매개 변수로 작업 메서드에 삽입을 하는 것이 적절할 수 있습니다. 이는 다음과 같이 `[FromServices]` 특성으로 매개 변수를 표시하여 수행됩니다.

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=1&range=33-38)]

## <a name="accessing-settings-from-a-controller"></a>컨트롤러에서 설정 액세스

컨트롤러 내에서 응용 프로그램 또는 구성 설정에 액세스하는 것은 일반적인 패턴입니다. 이 액세스는 [구성](xref:fundamentals/configuration/index)에 설명된 옵션 패턴을 사용해야 합니다. 일반적으로 종속성 주입을 사용하여 컨트롤러에서 직접 설정을 요청해서는 안 됩니다. 더 나은 방법은 `IOptions<T>` 인스턴스를 요청하는 것입니다. 여기서 `T`란 필요한 구성 클래스입니다.

옵션 패턴을 사용하려면 다음과 같은 옵션을 나타내는 클래스를 만들어야 합니다.

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Model/SampleWebSettings.cs)]

그런 다음, 옵션 모델을 사용하도록 응용 프로그램을 구성하고, 구성 클래스를 `ConfigureServices`의 서비스 컬렉션에 추가해야 합니다.

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=3,4,5,6,9,16,19&range=14-44)]

> [!NOTE]
> 위의 목록에서 JSON 형식 파일에서 설정을 읽도록 응용 프로그램을 구성하는 중 입니다. 또한 위의 주석으로 처리된 코드에 표시된 대로 코드에서 완전히 설정을 구성할 수 있습니다. 추가 구성 옵션은 [구성](xref:fundamentals/configuration/index)을 참조하세요.

강력한 형식의 구성 개체를 지정하고(이 경우 `SampleWebSettings`) 서비스 컬렉션에 추가하고 나면, `IOptions<T>`의 인스턴스(이 경우 `IOptions<SampleWebSettings>`)를 요청하여 모든 컨트롤러 또는 작업 메서드에서 이를 요청할 수 있습니다 . 다음 코드는 컨트롤러에서 설정을 요청하는 방법 중 하나를 보여 줍니다.

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/SettingsController.cs?highlight=3,5,7&range=7-22)]

옵션 패턴을 따르면 설정 및 구성을 서로 분리할 수 있으며, 컨트롤러가 [문제의 분리](http://deviq.com/separation-of-concerns/)를 따르고 있는지 확인합니다. 컨트롤러는 설정 정보를 찾는 방법이나 위치를 알 필요가 없기 때문입니다. 또한 컨트롤러가 더 쉽게 [컨트롤러 논리 테스트](testing.md)를 단위 테스트할 수 있습니다. 컨트롤러 클래스 내 설정 클래스의 [정적 집착](http://deviq.com/static-cling/) 또는 직접 인스턴스화가 없기 때문입니다.
